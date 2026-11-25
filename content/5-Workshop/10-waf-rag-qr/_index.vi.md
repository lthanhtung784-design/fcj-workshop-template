---
title: "WAF, RAG và giải mã QR"
weight: 10
---

[PhishGuard-WAF-RAG-QR.zip](/downloads/PhishGuard-WAF-RAG-QR.zip)

Bắt đầu trên stack PhishGuard demo đang chạy ở us-east-1, profile phishguard, chế độ DRY_RUN. File này hướng dẫn thao tác trên Windows. Các kết quả live bên dưới là tiêu chí để người vận hành kiểm tra. Gói có mã và mẫu đã thử cục bộ. Các thao tác deploy WAF, ingest tài liệu và gửi report phát sinh hoạt động trên tài khoản của bạn.

## Chuẩn bị PowerShell

Giải nén PhishGuard-WAF-RAG-QR.zip vào Downloads\PhishGuard-WAF-RAG-QR. Mở PowerShell từ thư mục project PhishGuard đang deploy. Nếu đang xem hướng dẫn từ gói GitHub, tải ZIP tính năng tại trang Workshop, mục WAF, RAG và giải mã QR.

```powershell
$kit = "$env:USERPROFILE\Downloads\PhishGuard-WAF-RAG-QR"
$project = "$env:USERPROFILE\Projects\phishguard-ai"
Set-Location $project
Test-Path (Join-Path $kit 'infra\phishguard-waf.yaml')
Test-Path .\src\ocr.py
$profileName = 'phishguard'
$region = 'us-east-1'
$stackName = 'phishguard-ai'
$awsOpts = @('--profile',$profileName,'--region',$region,'--no-cli-pager')
aws sts get-caller-identity @awsOpts
if ($LASTEXITCODE -ne 0) { throw 'Kiểm tra phiên đăng nhập AWS.' }
$stackJson = aws cloudformation describe-stacks --stack-name $stackName @awsOpts --output json
if ($LASTEXITCODE -ne 0) { throw 'Không đọc được stack.' }
$stack = (($stackJson -join "`n") | ConvertFrom-Json).Stacks[0]
$outputs = @{}
foreach ($row in $stack.Outputs) { $outputs[$row.OutputKey] = $row.OutputValue }
$params = @{}
foreach ($row in $stack.Parameters) { $params[$row.ParameterKey] = $row.ParameterValue }
$site = ([string]$params['CloudFrontOrigin']).TrimEnd('/')
$dist = $params['CloudFrontDistributionId']
$site
$dist
$params['ContainmentMode']
```

Kiểm tra hai Test-Path là True, site và Distribution ID trùng PhishGuard-Web, containment là DRY_RUN. Nếu dùng bản lab hoàn chỉnh trong site ZIP mới, mã QR đã được tích hợp sẵn. Khi dùng bản project riêng đang deploy, kiểm đúng phiên bản OCR Tesseract trước khi áp patch ở mục 3.

## 1. Cấu hình và kiểm thử WAF

Ảnh tab Security với bốn mục Not enabled đủ ghi nhận mốc trước khi làm. Không cần chạy lại get-distribution-config để bắt đầu. CloudFront trong ảnh dùng Pay-as-you-go. Mẫu CloudFormation riêng tạo một Web ACL scope CLOUDFRONT ở us-east-1. Việc gắn ACL vào distribution là một bước riêng. EnableWaf trong SAM hiện là tham số mô tả.

**1a. Tạo Web ACL ban đầu ở Count.** Chạy trong cùng cửa sổ PowerShell. Nếu profile thiếu quyền, người phụ trách stack edge thực hiện bằng role được phép triển khai CloudFormation/WAF. COUNT và probe thử nghiệm vẫn thuộc tài nguyên tính phí.

```powershell
function Set-PgWaf([string]$mode,[string]$probe) {
  aws cloudformation deploy --stack-name phishguard-edge-waf --template-file (Join-Path $kit 'infra\phishguard-waf.yaml') --parameter-overrides "ProtectionMode=$mode" "ProbeMode=$probe" RequestsPerMinute=120 --no-fail-on-empty-changeset @awsOpts
  if ($LASTEXITCODE -ne 0) { throw 'Kiểm tra Events của phishguard-edge-waf.' }
}
Set-PgWaf COUNT COUNT
$acl = aws cloudformation describe-stacks --stack-name phishguard-edge-waf --query "Stacks[0].Outputs[?OutputKey=='WebACLArn'].OutputValue | [0]" --output text @awsOpts
if ($LASTEXITCODE -ne 0 -or !$acl -or $acl -eq 'None') { throw 'Chưa lấy được Web ACL ARN.' }
$acl
```

Mẫu có default Allow, AWSManagedRulesCommonRuleSet và một rate-based rule theo IP cho POST đúng hai đường /api/reports, /api/uploads/presign. Ngưỡng lab 120 request/60 giây là điểm khởi đầu, cần chỉnh theo số nhân viên dùng chung IP. Nhóm managed dùng override kết quả nhóm sang Count, rate rule cũng Count. Rule tạm WorkshopHeaderProbe chỉ khớp đường / cùng header x-phishguard-workshop: verify-edge. Probe không cần token hoặc gửi incident. Sampled requests tắt để hạn chế ghi nhận nội dung người dùng, CloudWatch metrics bật.

**1b. Liên kết đúng distribution.** Trong AWS WAF chọn phạm vi Global (CloudFront), mở Web ACL có ARN ở trên, vào Associated AWS resources → Add AWS resources → chọn đúng PhishGuard-Web và xác nhận. Có thể dùng phần Security của distribution nếu console cho chọn existing web ACL. Chọn ACL đã tạo để các rule và tham số trong hướng dẫn khớp. Nếu màn hình báo distribution đã gắn ACL khác, xem lại ACL đang dùng trước khi thay. Khi đã xác định đúng tài nguyên và console thiếu thao tác này, AWS CLI v2 hiện hành cũng hỗ trợ:

```powershell
aws cloudfront associate-distribution-web-acl --id $dist --web-acl-arn $acl @awsOpts
```

Chỉ cần liên kết một lần qua console hoặc CLI. Chờ distribution hoàn tất triển khai, rồi chụp mục associated resources chứa distribution và trang Rules. Nếu CLI báo invalid choice, dùng console hoặc cập nhật AWS CLI v2.

**1c. Thử đường bình thường.** Gọi hai lệnh trước và sau khi cập nhật rule. Lần đầu kỳ vọng 200 cho cả hai ở default root của SPA. Tra CountedRequests của PhishGuardProbe (AWS/WAFV2, CloudWatch N. Virginia cho CloudFront); chờ metric cập nhật. Metric probe chứng minh request thử đi qua ACL.

```powershell
curl.exe -s -o NUL -w "%{http_code}\n" "$site/"
curl.exe -s -o NUL -w "%{http_code}\n" -H "x-phishguard-workshop: verify-edge" "$site/"
```

**1d. Chứng minh Block an toàn.** Chạy `Set-PgWaf COUNT BLOCK`. Sau khi cấu hình lan truyền, gọi lại hai lệnh trên. Lệnh thường vẫn phải **200**, lệnh có header phải **403**. Đối chiếu BlockedRequests của PhishGuardProbe và chụp kèm hai kết quả. Nếu cả hai vẫn 200, kiểm tra propagation, đúng hostname và ACL association. Phép thử này xác nhận cơ chế chặn ở edge; chưa đo ngưỡng của rate rule.

**1e. Kiểm tra giao dịch thật trước khi áp dụng luật.** Với managed group và rate rule vẫn Count, đăng nhập reporter, gửi một thông báo bình thường (202), upload PNG (presign 201, POST S3 204), gửi một fixture EML có nội dung đáng ngờ, mở chi tiết và thử dashboard admin. So thời điểm với metric của CommonRules. File upload POST tới S3 nằm ngoài đường CloudFront. Khi bật enforcement, API Gateway vẫn cần JWT và phân quyền. Nếu request nghiệp vụ bị khớp, giữ Count cho đến khi xác định subrule và chỉnh ngoại lệ đúng phạm vi trước khi thử lại.

**1f. Kết thúc.** Dùng `Set-PgWaf ENFORCE OFF` khi các ca hợp lệ đã đạt: managed rules dùng action của AWS, rate rule Block, probe được bỏ. Chạy lại bộ ca 1e, hai lần GET ở 1c giờ đều trở về 200. Nếu thấy request hợp lệ lỗi, chạy `Set-PgWaf COUNT OFF` để trở lại quan sát. Ghi lại ngày, mode, rate limit, ID distribution, ảnh Rules/metrics sau cùng. Chỉ cập nhật sơ đồ “đã triển khai” khi association đã xong. Với 20.000 request/tháng, 1 ACL và 2 mục luật tính phí, WAF minh họa khoảng 7,01 USD/tháng trước thuế. Probe tạm tạo thêm một mục luật trong thời gian bật. Khi đóng lab vĩnh viễn, người quản lý gỡ association khỏi đúng distribution trước khi xóa stack edge.

[AWS WAF testing](https://docs.aws.amazon.com/waf/latest/developerguide/web-acl-testing.html) · [Rate-based rules](https://docs.aws.amazon.com/waf/latest/developerguide/waf-rule-statement-type-rate-based.html) · [AWS CLI association](https://docs.aws.amazon.com/cli/latest/reference/cloudfront/associate-distribution-web-acl.html) · [WAF pricing](https://aws.amazon.com/waf/pricing/)

Nếu cần minh chứng riêng cho giới hạn tốc độ, chỉnh tham số RequestsPerMinute xuống 10 trên distribution demo riêng, giữ rule ở Count. Trong cửa sổ 60 giây, gửi hơn 10 POST thử từ cùng IP tới một trong hai route có scope, dùng request chưa đăng nhập để API từ chối trước khi tạo incident. Quan sát CountedRequests của PhishGuardSubmissionRate và so với GET dashboard nằm ngoài scope. AWS thực thi mức giới hạn gần đúng và có độ trễ. Ghi “chưa quan sát” nếu metric chưa ghi nhận. Khôi phục 120 và chờ propagation trước khi chạy các ca nghiệm thu hoặc chuyển ENFORCE. Thử header ở mục 1d là đủ cho demo cơ chế block mà không tạo tải trên portal đang có người dùng.

## 2. Bổ sung playbook và kiểm tra RAG

**Mốc trước thay đổi.** Đăng nhập reporter. Upload riêng fixtures/phase-h/H05-return-path.eml và H11-manual-review.eml trên portal. Ghi mã incident, kết quả xác thực hoặc trạng thái, trạng thái tổng hợp, tên nguồn thực sự được trích và bước xử lý được gợi ý. Có thể dùng incident trước đó của cùng bản deploy. Kiểm tra top 3 bằng công cụ chỉ đọc:

```powershell
$python = Join-Path $project '.venv\Scripts\python.exe'
$kb = $params['KnowledgeBaseId']
if (!$kb) { throw 'Xem KnowledgeBaseId trong Parameters hoặc Bedrock → Knowledge Bases.' }
& $python (Join-Path $kit 'tools\check_playbooks.py') --kb $kb --profile $profileName
```

**Upload hai file.** Gói có sẵn 04-email-chuyen-tiep-va-dmarc.txt và 05-high-thieu-muc-tieu.txt. Lưu một bản trong source project và một bản dưới đúng prefix playbooks/ của data source.

```powershell
$kbBucket = $outputs['KbDocsBucketName']
if (!$kbBucket) { throw 'Thiếu KbDocsBucketName.' }
$docs = Get-ChildItem (Join-Path $kit 'kb-docs\playbooks\*.txt')
foreach ($doc in $docs) {
  Copy-Item $doc.FullName (Join-Path "$project\kb-docs\playbooks" $doc.Name)
  aws s3 cp $doc.FullName "s3://$kbBucket/playbooks/$($doc.Name)" @awsOpts
  if ($LASTEXITCODE -ne 0) { throw "Upload thất bại: $($doc.Name)" }
}
```

Trong **Bedrock → Knowledge Bases → KB đúng ID → Data source**, kiểm S3 bucket/prefix, chọn **Sync**, chờ ingestion job **COMPLETE** và kiểm số file lỗi bằng 0. Không cần tạo lại KB hay vector index. Chạy lại lệnh check_playbooks.py phía trên. Kỳ vọng H05 lấy được tài liệu 04, H11 lấy được tài liệu 05 trong top 3. Kết quả false sau sync là một retrieval miss cần ghi nhận.

Gửi hai fixture thành hai report mới qua web. Đối chiếu với trước khi sync. H05 vẫn INDETERMINATE; giải thích tốt sẽ đề nghị xin EML gốc/tra log thư nhận ban đầu. H11 vẫn NEEDS_REVIEW khi thiếu mục tiêu; giải thích tốt chỉ ra bằng chứng cần bổ sung và người phụ trách. Ghi tên file hoặc nguồn hiện thực tế. Check script hỏi bằng câu của analyst; ứng dụng tạo truy vấn từ các luật kích hoạt. Hai danh sách có thể khác nhau. Nếu có FALLBACK, ghi fallback_reason và kiểm riêng bước Retrieve. Giữ nguyên điểm do policy chấm khi đối chiếu. Source ID như KB-1 phụ thuộc lượt Retrieve nên dùng tên file để so sánh. [Đồng bộ Bedrock data source](https://docs.aws.amazon.com/bedrock/latest/userguide/kb-data-source-sync-ingest.html)

## 3. Giải mã QR trong ảnh

Bản bổ sung đọc mã QR cục bộ trong Lambda ExtractRedact. Nó chấp nhận URL HTTP/HTTPS, bỏ query và fragment, bỏ payload có thông tin đăng nhập, đưa host/path đã vô hiệu hóa qua bộ che PII và policy hiện có. Thư viện xử lý ảnh không truy cập mạng theo URL đã giải mã. Mỗi ảnh tối đa tám URL khác nhau; giới hạn pixel và OCR tiếng Việt vẫn áp dụng. QR phi URL như Wi-Fi, danh thiếp hoặc một chuỗi chữ được bỏ qua. Confidence và số ký tự vẫn đo OCR; một URL QR hợp lệ cho phép workflow đi tiếp dù OCR thiếu chữ. Việc có QR tự nó không cộng điểm.

### 3a. Chọn đúng nguồn

- **Dự án Windows hiện có** với lớp OCR tiếng Việt: áp patch bên dưới từ thư mục gốc của app. Đóng gói kèm một Lambda Layer riêng cho CPython 3.12 Linux x86_64, zxing-cpp 2.3.0. Giữ đúng kiến trúc x86_64 khi build.
- **PhishGuard-Lab.zip trong bản site mới**: các thay đổi đã có sẵn ở lab/. Dùng lab làm thư mục project và tiếp tục ở 3b sau khi đã có venv, profile và stack theo Workshop.
- Bản project có thay đổi riêng: git apply --check kiểm tra trước khi ghi. Nếu lỗi, xem diff của src/ocr.py, src/extract_redact.py, template.yaml và frontend/src/lib/backend-contract.ts, ghép các hunk tương ứng. Bản vá dùng trên phiên bản Tesseract của Workshop.

```powershell
Set-Location $project
$patch = Join-Path $kit 'qr-integration.patch'
git apply --check --ignore-space-change $patch
if ($LASTEXITCODE -ne 0) { throw 'Kiểm tra phiên bản source hoặc xem patch đã được áp chưa.' }
git apply --ignore-space-change $patch
if ($LASTEXITCODE -ne 0) { throw 'Áp patch QR chưa thành công.' }
Copy-Item (Join-Path $kit 'layers\qr-py312-x86_64.zip') .\layers\
```

### 3b. Build và cập nhật stack ứng dụng

Giữ đúng commit và bộ tham số của stack đang chạy. Script đọc lại tham số mới nhất ngay trước khi deploy. Chỉ áp dụng cho template PhishGuard demo. Nếu bạn vừa cấu hình WAF ở stack edge, bước này không cần đổi EnableWaf. SAM build có thể cần Docker với `--use-container` nếu dependency máy Windows không phù hợp.

```powershell
Set-Location $project
Test-Path .\layers\qr-py312-x86_64.zip
sam validate --lint --template-file template.yaml --region $region --profile $profileName
if ($LASTEXITCODE -ne 0) { throw 'Template không hợp lệ.' }
sam build --template-file template.yaml
if ($LASTEXITCODE -ne 0) { throw 'SAM build lỗi.' }
$live = aws cloudformation describe-stacks --stack-name $stackName @awsOpts --output json
if ($LASTEXITCODE -ne 0) { throw 'Không đọc được stack hiện hành.' }
$now = (($live -join "`n") | ConvertFrom-Json).Stacks[0]
$overrides = @(foreach ($p in $now.Parameters) {
  if ([string]$p.ParameterValue -ne '') { "$($p.ParameterKey)=$($p.ParameterValue)" }
})
$artifactBucket = $outputs['IntakeBucketName']
if (!$artifactBucket -or !$overrides.Count) { throw 'Thiếu bucket hoặc tham số stack.' }
sam deploy --template-file .aws-sam/build/template.yaml --stack-name $stackName --region $region --profile $profileName --s3-bucket $artifactBucket --s3-prefix sam-artifacts --capabilities CAPABILITY_NAMED_IAM --parameter-overrides @overrides --confirm-changeset --no-fail-on-empty-changeset
if ($LASTEXITCODE -ne 0) { throw 'Kiểm tra CloudFormation Events.' }
```

Kiểm tra change set gồm layer QR, ExtractRedact và workflow có thay đổi. Các Lambda khác có thể Modify vì dùng chung thư mục mã. Xác nhận khi đúng phạm vi. Chờ UPDATE_COMPLETE. Kiểm tra ExtractRedact có cả layer OCR và layer QR. Để trang web hiển thị nhãn “Đã đọc URL từ QR”, build/deploy frontend từ cùng bản source. Dùng file frontend/.env.production.local đã thiết lập với VITE_USE_MOCK=false của deployment hiện hành. Từ lab mới, tạo cấu hình này theo chương Triển khai cổng báo cáo trước khi build.

```powershell
Push-Location (Join-Path $project 'frontend')
try {
  npm ci
  if ($LASTEXITCODE -ne 0) { throw 'npm ci lỗi.' }
  npm run build
  if ($LASTEXITCODE -ne 0) { throw 'Vite build lỗi.' }
  $webBucket = $outputs['WebBucketName']
  if (!$webBucket) { throw 'Thiếu web bucket.' }
  aws s3 sync .\dist\ "s3://$webBucket/" --exclude index.html @awsOpts
  if ($LASTEXITCODE -ne 0) { throw 'Không tải được asset.' }
  aws s3 cp .\dist\index.html "s3://$webBucket/index.html" --content-type text/html --cache-control no-cache @awsOpts
  if ($LASTEXITCODE -ne 0) { throw 'Không tải được index.html.' }
} finally { Pop-Location }
aws cloudfront create-invalidation --distribution-id $dist --paths '/' '/index.html' @awsOpts
```

### 3c. Thử bằng file thật

Mở tab Tải lên bằng chứng trên CloudFront. Mỗi file là một incident mới. Giữ incident ID và chụp phần bằng chứng ở trang chi tiết.

| File trong fixtures/qr/ | Đối chiếu |
|---|---|
| qr-url.png | Ảnh chỉ có QR. Phần văn bản có QR và IOC hxxps://example[.]org/workshop/qr. Query demo và fragment đã bị bỏ. Workflow đi qua Triage dù OCR không đọc ra chữ; nếu blocklist không có IOC liên quan, kỳ vọng LOW/NO_ACTION. |
| blank.png | Không trích được URL hay chữ, NEEDS_MORE_INFO, chưa chấm điểm. |
| qr-text.png | QR chứa một chuỗi chữ phi URL, mẫu không có chữ in đọc được, NEEDS_MORE_INFO. |
| DEMO_1 của portal | OCR vie+eng và luật vẫn chạy như trước; đối chiếu với số điểm của chính deployment. |

Nếu ảnh QR vào NEEDS_MORE_INFO, kiểm tra phiên bản execution mới và qr_url_count ở output ExtractRedact. Nếu báo Runtime.ImportModuleError, kiểm tra cả hai Layers và runtime/architecture, sau đó xem CloudWatch log của đúng Lambda. Nếu extract đúng nhưng giao diện còn nhãn cũ, kiểm tra asset build mới và invalidation. Rút lại tính năng bằng cách triển khai lại bản source trước thay đổi với cùng tham số, sau khi xem xét change set và các execution đang chạy.

## 4. Chạy website tài liệu trên máy

## Chạy website FCAJ trên Windows trước khi push

Website tài liệu dùng Hugo và mở được trên máy không đăng nhập AWS. Để đăng nhập Reporter và gửi incident, mở địa chỉ CloudFront của ứng dụng. Hai website phục vụ hai mục đích khác nhau.

### 1. Giải nén đúng thư mục

Tải PhishGuard-FCAJ-GitHub.zip vào Downloads. Mở PowerShell, dùng một thư mục trống để giữ bản đang chỉnh sửa của bạn.

```powershell
$siteZip = "$env:USERPROFILE\Downloads\PhishGuard-FCAJ-GitHub.zip"
$dest = "$env:USERPROFILE\Projects\PhishGuard-docs-preview"
Expand-Archive -LiteralPath $siteZip -DestinationPath $dest -ErrorAction Stop
Set-Location "$dest\fcaj-workshop"
Test-Path .\config.toml
Test-Path .\themes\hugo-theme-learn
```

Cả hai dòng phải trả True. Nếu đã giải nén qua File Explorer, mở PowerShell tại thư mục chứa config.toml rồi tiếp tục. Nếu trình duyệt đã thêm (1) vào tên ZIP, sửa tên ở dòng đầu.

### 2. Cài Hugo Extended 0.134.3

Trên Windows x64, tải bản portable cùng phiên bản với GitHub Actions. Chạy trong cùng cửa sổ, không cần quyền Administrator.

```powershell
$version = '0.134.3'
$toolsDir = "$env:LOCALAPPDATA\Programs\HugoExtended\$version"
$hugoZip = "$env:TEMP\hugo_extended_${version}_windows-amd64.zip"
$release = "https://github.com/gohugoio/hugo/releases/download/v$version"
Invoke-WebRequest "$release/hugo_extended_${version}_windows-amd64.zip" -OutFile $hugoZip -ErrorAction Stop
Expand-Archive -LiteralPath $hugoZip -DestinationPath $toolsDir -Force -ErrorAction Stop
$hugo = Join-Path $toolsDir 'hugo.exe'
& $hugo version
```

Kiểm tra kết quả có v0.134.3 và extended. Có thể tải cùng ZIP từ trang release bằng trình duyệt và giải nén thủ công nếu PowerShell bị chặn tải. Bản binary đã giải nén sử dụng được ở các lần sau.

### 3. Mở trang và xem thay đổi

```powershell
& $hugo server --disableFastRender --bind 127.0.0.1 --port 1313
```

Giữ cửa sổ đang chạy. Mở http://localhost:1313/ cho tiếng Anh hoặc http://localhost:1313/vi/ cho tiếng Việt. Chọn Workshop → WAF, RAG và giải mã QR. Sửa một tiêu đề trong content rồi lưu, kiểm tra trình duyệt tự tải lại. Nhấn Ctrl+C để dừng. Nếu cổng bận, thay 1313 bằng 1314 trong cả câu lệnh và địa chỉ trình duyệt. Nếu mở PowerShell mới, quay lại thư mục có config.toml và đặt lại `$hugo = "$env:LOCALAPPDATA\Programs\HugoExtended\0.134.3\hugo.exe"`.

### 4. Kiểm tra bản xuất trước khi push

```powershell
& $hugo --minify
if ($LASTEXITCODE -ne 0) { throw 'Hugo build failed.' }
Test-Path .\public\vi\5-workshop\index.html
```

Kết quả cuối là True. Commit nguồn trên main theo phần GitHub Pages của README. GitHub Actions tạo lại thư mục public khi xuất bản. Theme đã có trong ZIP. Nếu muốn dùng Git để push và máy chưa có Git, cài bằng `winget install --id Git.Git -e`, mở lại PowerShell rồi chạy `git --version`.

[Tải Hugo v0.134.3](https://github.com/gohugoio/hugo/releases/tag/v0.134.3) · [Cài Hugo cho Windows](https://gohugo.io/installation/windows/)

