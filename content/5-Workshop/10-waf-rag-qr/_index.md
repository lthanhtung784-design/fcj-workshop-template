---
title: "CloudFront WAF, playbooks and QR images"
weight: 10
---

Use [PhishGuard-WAF-RAG-QR.zip](/downloads/PhishGuard-WAF-RAG-QR.zip) for the incremental patch, native Linux QR layer, two playbooks, test fixtures and WAF template. Extract to Downloads/PhishGuard-WAF-RAG-QR. Work from the existing Tesseract-based demo project in the same PowerShell session. The following are live acceptance criteria. The account owner performs deployment and association.

## Account and distribution

Check the caller identity, project folder, exact CloudFront site/distribution and DRY_RUN mode.

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

## Configure and test WAF

The CloudFront Security screenshot is a suitable starting record. Deploy the separate CloudFormation stack in us-east-1. Start the basic managed group and IP rate rule in Count. The rate rule covers POST /api/reports and /api/uploads/presign, initially 120 per IP in 60 seconds. Browser-to-S3 file uploads use a separate path. A temporary probe matches a workshop header on /. Metrics are enabled and sampled requests are disabled.

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

In AWS WAF, choose Global (CloudFront), find the returned ARN, then add just the intended distribution under Associated AWS resources. If another ACL is already associated, inspect it before changing the association. As an alternative, use a current AWS CLI v2 with the following command. Wait for the distribution to deploy.

```powershell
aws cloudfront associate-distribution-web-acl --id $dist --web-acl-arn $acl @awsOpts
```

The unmarked and marked GET should both return 200 in Count. Check PhishGuardProbe CountedRequests in us-east-1.

```powershell
curl.exe -s -o NUL -w "%{http_code}\n" "$site/"
curl.exe -s -o NUL -w "%{http_code}\n" -H "x-phishguard-workshop: verify-edge" "$site/"
```

Run `Set-PgWaf COUNT BLOCK`, allow propagation and repeat the two GETs. Expect 200 without the header and 403 with it. Check BlockedRequests. This only demonstrates the temporary probe. For regression, sign in, send ordinary text, upload a PNG and a suspicious sample, and open the admin dashboard. Review rule metrics for legitimate matches. For rate observation, the guide includes a separate Count-mode test on an isolated lab distribution. When legitimate workflows pass, run `Set-PgWaf ENFORCE OFF`. Repeat functional tests. To roll back enforcement, use `Set-PgWaf COUNT OFF`. Save the association, rule modes and timestamps as evidence. The temporary probe adds one rule while present. Under the workshop assumptions, the permanent WAF is about USD 7.01/month.

## Extend the Knowledge Base

Capture H05 and H11 incident IDs, score, synthesis status and actual citations first. Run this read-only top-three retrieval check.

```powershell
$python = Join-Path $project '.venv\Scripts\python.exe'
$kb = $params['KnowledgeBaseId']
if (!$kb) { throw 'Xem KnowledgeBaseId trong Parameters hoặc Bedrock → Knowledge Bases.' }
& $python (Join-Path $kit 'tools\check_playbooks.py') --kb $kb --profile $profileName
```

Upload exactly the two new documents to the current playbooks prefix.

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

Open Bedrock → Knowledge Bases → the stack KB → the existing S3 data source → Sync. Wait for COMPLETE and zero failed documents. Run the retrieval check again, then resubmit both EML fixtures as new reports. Look for 04 in the analyst query for H05 and 05 for H11. The portal uses deterministic rule text to query, so UI citations may differ. Record the actual source, action guidance and fallback reason. Expected business outcomes remain INDETERMINATE for original H05 authentication and NEEDS_REVIEW for H11 without a valid target.

## Decode QR in an image

For an existing project run the patch check and apply at its root. The full lab bundle already includes this change. The additional layer targets Linux CPython 3.12 x86_64.

```powershell
Set-Location $project
$patch = Join-Path $kit 'qr-integration.patch'
git apply --check --ignore-space-change $patch
if ($LASTEXITCODE -ne 0) { throw 'Kiểm tra phiên bản source hoặc xem patch đã được áp chưa.' }
git apply --ignore-space-change $patch
if ($LASTEXITCODE -ne 0) { throw 'Áp patch QR chưa thành công.' }
Copy-Item (Join-Path $kit 'layers\qr-py312-x86_64.zip') .\layers\
```

Build and review the SAM change set, preserving deployed parameters. Expect the QR layer, ExtractRedact and a workflow change. Wait for UPDATE_COMPLETE and verify both OCR and QR layers.

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

With the existing production Vite configuration, upload new assets before index.html and invalidate the entry page.

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

Upload fixtures/qr/qr-url.png. It contains only a QR. Expect the defanged IOC hxxps://example[.]org/workshop/qr with query and fragment removed. With a clean blocklist, expect LOW and NO_ACTION. Upload blank.png and qr-text.png separately; both should reach NEEDS_MORE_INFO. Compare DEMO_1 with its previous OCR result. QR URLs go through the existing policy engine without navigation. Up to eight unique HTTP(S) URLs are retained; embedded credentials and non-web payloads are skipped. OCR confidence continues to describe only visible text.

## Local documentation preview

Install Hugo Extended 0.134.3 for Windows x64, matching the Pages workflow. The release ZIP carries a portable executable. In the repository root (the folder containing config.toml), follow the commands below. English is available at http://localhost:1313/ and Vietnamese at http://localhost:1313/vi/. Ctrl+C stops the server. Use port 1314 if 1313 is in use. The local documentation requires no AWS credentials.

```powershell
$siteZip = "$env:USERPROFILE\Downloads\PhishGuard-FCAJ-GitHub.zip"
$dest = "$env:USERPROFILE\Projects\PhishGuard-docs-preview"
Expand-Archive -LiteralPath $siteZip -DestinationPath $dest -ErrorAction Stop
Set-Location "$dest\fcaj-workshop"
Test-Path .\config.toml
Test-Path .\themes\hugo-theme-learn
```

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

```powershell
& $hugo server --disableFastRender --bind 127.0.0.1 --port 1313
```

```powershell
& $hugo --minify
if ($LASTEXITCODE -ne 0) { throw 'Hugo build failed.' }
Test-Path .\public\vi\5-workshop\index.html
```

