# 📄 Documents and S3

**Understand well:** S3 stores original files. A prefix is a folder-like part of an object name. Uploading is separate from KB sync.

## 🧪 Small test dataset

No existing sample runbooks were found in this project. Two fictional samples are prepared for your review:

- [Staging rollback](../data/runbooks/staging-api-rollback.txt): namespace, approval, rollback, and verification.
- [Production rollback](../data/runbooks/production-api-rollback.txt): pipeline-only rollback with different approval.

Do not execute the Kubernetes commands; they are test content for retrieval. Review and approve these files before uploading. Environment metadata/filtering will be configured when we connect the KB data source.

| Question | Expected evidence/answer |
| --- | --- |
| How do I roll back the staging API? | Staging source; check context/history and approval before rollback |
| How long should I wait for staging rollout status? | 120 seconds |
| Can I use the staging rollback command in production? | No; production uses the approved pipeline and incident-commander approval |
| How do I recover a deleted production database? | Missing evidence; neither document defines recovery |
| Is the staging cluster healthy right now? | Cannot determine live status from these documents |

These are expected results, not observed chatbot answers.

## ▶️ Execute

Follow steps **05–08** in the [CLI sequence](03_cli_execution.md). Budget setup was skipped by user choice. S3 requests and storage are billable; these two tiny text files should cost only a small fraction of a dollar for one day, excluding unrelated account usage. No embedding or vector-store charges begin from this upload alone.

Observed on 2026-09-27: public-access blocking and AES256 encryption verified through read-only calls. User-provided upload output and S3 listing confirm two nonempty runbooks: production 859 bytes, staging 1093 bytes. Remote contents have not been hash-compared. KB ingestion has not started.

## 🎤 Interview FAQ

**1. Is S3 the vector database?** No; it holds original documents.

**2. Does uploading automatically update our KB?** No; we start a sync after connecting the data source.

**3. Why test staging and production together?** Similar wording can hide different approvals and procedures.

**4. Why ask an unsupported question?** To test whether the chatbot acknowledges missing evidence.

**5. Why keep the dataset small?** It makes retrieved passages easier to inspect and limits ingestion costs.
