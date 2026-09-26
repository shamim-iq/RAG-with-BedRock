# ▶️ AWS CLI execution sequence

Run from the project root in PowerShell. Replace `<...>` placeholders before running. `<aws-profile>` means your deployment profile; `<read-only-profile>` means your inspection profile. Keep actual values in ignored `.local/` files.

Run one step at a time. Stop on errors. Record date, step number, exit code, and a sanitized result in local `PROGRESS.md`. Add each created resource to the local cleanup inventory.

| Order | Activity | Execution |
| --- | --- | --- |
| 01 | Check identity and service access | Initial read-only checks verified |
| 02–04 | Budget setup | Skipped by user choice; no budget created |



Later deployment commands will be added as we reach them.

**Next sequence:** 05 review files → 06 create bucket → 07 verify privacy/encryption → 08 upload and inspect.

## 01 · Check identity and access

**Purpose:** confirm the expected account and inspection access. **Cost:** no resources created or model calls.

```powershell
aws sts get-caller-identity --profile "<read-only-profile>" --no-cli-pager
aws bedrock list-foundation-models --by-provider Amazon --region us-east-1 --profile "<read-only-profile>" --query 'modelSummaries[].modelId' --no-cli-pager
aws bedrock-agent list-knowledge-bases --region us-east-1 --profile "<read-only-profile>" --query 'length(knowledgeBaseSummaries)' --no-cli-pager
aws opensearchserverless list-collections --region us-east-1 --profile "<read-only-profile>" --query 'length(collectionSummaries)' --no-cli-pager
```

**Expected:** matching identity, model IDs, and resource counts. Keep identity output private. These calls do not prove deployment or invocation access.

## 02–04 · Budget setup skipped

User chose rough estimates and same-day cleanup for this one-day lab. No budget was created. Verify vector-store rates/capacity before provisioning it.

**Dummy example only — not configured:** USD 10/month, email `learner@example.com`, alerts above 50% (USD 5) and 80% (USD 8). A budget alert does not cap spending.

## 05 · Review the source files

**Purpose:** approve the two fictional [runbooks and expected answers](04_documents_and_s3.md). **Cost:** none locally. Do not execute their Kubernetes commands.

```powershell
Get-Content data/runbooks/staging-api-rollback.txt
Get-Content data/runbooks/production-api-rollback.txt
```

**Expected:** staging and production procedures are clearly different; no secrets or personal data.

## 06 · Create the lab bucket

**Purpose:** hold the original documents. Use `<bucket-name>` = `rag-bedrock-<account-id>-us-east-1` to match your local IAM policy. Replace both placeholders locally. If the name is unavailable, stop; changing it also requires updating the local policies.

**Cost:** S3 storage and requests. For two tiny text files kept one day, expect a small fraction of a dollar, not a free-tier guarantee. No OpenSearch or model resources are created.

First confirm the deployment identity locally and check for an existing bucket:

```powershell
aws sts get-caller-identity --profile "<aws-profile>" --no-cli-pager
aws s3api head-bucket --bucket "<bucket-name>" --expected-bucket-owner "<account-id>" --profile "<aws-profile>" --region us-east-1 --no-cli-pager
```

Proceed only for `404 Not Found`. If successful, the bucket exists: stop and confirm ownership/purpose before reuse. For `403` or another error, stop and investigate.

```powershell
aws s3api create-bucket --bucket "<bucket-name>" --region us-east-1 --profile "<aws-profile>" --no-cli-pager
```

**Expected:** a bucket location and exit code 0. `us-east-1` does not use `LocationConstraint` here. Record the bucket and creation time in `.local/resource-inventory.md` immediately for cleanup.

## 07 · Confirm privacy and encryption

**Purpose:** keep documents private. **Cost:** configuration/read requests only; no paid model calls.

```powershell
aws s3api put-public-access-block --bucket "<bucket-name>" --public-access-block-configuration BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=true,RestrictPublicBuckets=true --expected-bucket-owner "<account-id>" --profile "<aws-profile>" --region us-east-1 --no-cli-pager
aws s3api get-public-access-block --bucket "<bucket-name>" --profile "<read-only-profile>" --region us-east-1 --no-cli-pager
aws s3api get-bucket-encryption --bucket "<bucket-name>" --profile "<read-only-profile>" --region us-east-1 --no-cli-pager
```

**Expected:** all four public-access settings `true`; default encryption shows `AES256`. If different, stop for review before uploading. Keep default ACL-disabled ownership and versioning disabled for this short lab.

## 08 · Upload and inspect

**Purpose:** place only the sample documents under `runbooks/`. **Cost:** two small uploads plus listing; no KB ingestion yet.

```powershell
aws s3 cp data/runbooks/ "s3://<bucket-name>/runbooks/" --recursive --exclude "*" --include "*.txt" --profile "<aws-profile>" --region us-east-1 --no-cli-pager
aws s3api list-objects-v2 --bucket "<bucket-name>" --prefix runbooks/ --query 'Contents[].{File:Key,Bytes:Size}' --profile "<read-only-profile>" --region us-east-1 --no-cli-pager
```

**Expected:** exactly two files, both nonempty. Record the result locally. Wait for verification before KB setup.

🧠 Check: Why does a successful S3 upload not mean the chatbot can answer from those files yet?

Sources: [Create bucket](https://docs.aws.amazon.com/cli/latest/reference/s3api/create-bucket.html), [Block public access](https://docs.aws.amazon.com/cli/latest/reference/s3api/put-public-access-block.html), [Upload](https://docs.aws.amazon.com/cli/latest/reference/s3/cp.html), [S3 pricing](https://aws.amazon.com/s3/pricing/).
