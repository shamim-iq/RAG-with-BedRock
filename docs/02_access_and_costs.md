# 🔐 AWS access and costs

**🟡 Current:** initial inspection checks passed after the policy update. Deployment access and cost review remain pending. No resources created or models invoked.

## ✅ Observed checks

| Check | Result |
| --- | --- |
| AWS CLI | 2.36.29 installed |
| Read-only identity | Expected account and IAM user verified |
| List Bedrock models | Passed; Titan V2 active with on-demand support |
| List Knowledge Bases | Passed on retry; zero in the selected Region |
| List OpenSearch collections | Passed; zero in the selected Region |
| Titan V2 availability | Region available; inspection caller not authorized for invocation |

Identity works; service permissions are separate. The user's attempt to apply the policy was denied: the deployment identity lacks `iam:PutUserPolicy`. Other deployment permissions and model invocation remain unverified.

## 🛠️ Next action: apply separate local policies

Two complete profile policies and application notes are maintained in ignored `.local/`. They are not published with this guide.

- **Codex:** inspection only; explicit deny outside the approved inspection actions.
- **User:** deployment, testing, ingestion, and cleanup through the deployment profile.
- An authorized IAM administrator applies them as **customer-managed policies** to the matching users. The earlier inline-policy command is superseded.
- User reported application; initial model/KB/collection inspection verified on 2026-09-27. Remaining inspection actions and deployment permissions are not yet tested.
- KB service-role permissions and OpenSearch access rules are separate setup requirements.

## 💰 Cost review before deployment

Follow [AWS CLI execution sequence](03_cli_execution.md) for the next manual activity: preparing documents and S3.

| Component | What incurs charges |
| --- | --- |
| S3 | Stored documents and requests |
| Titan embeddings | Text processed during ingestion and queries |
| Chat model | Input/output tokens; model not selected yet |
| OpenSearch Serverless | Compute capacity and storage |
| Later controls | Selected guardrail checks and monitoring/log storage |

**OpenSearch deserves special attention.** AWS currently distinguishes Classic collections (minimum ongoing compute, including a smaller dev/test option) from NextGen collections (idle compute can scale to zero). We must verify the chosen collection type and KB compatibility before estimating or creating it. Do not assume zero idle cost.

Planning formula: **compute unit-hours × regional rate + storage + model usage + requests**. Exact lab estimate remains pending model/collection selection and expected runtime. No cost cap is approved yet.

**Illustration, not a deployment quote:** at an assumed total of 1 OCU and $0.24 per OCU-hour, compute alone would cost $0.96 for 4 hours, $5.76 for 24 hours, or $175.20 for 730 hours. Actual capacity, regional rates, and storage/model charges must be checked before provisioning. A small budget alert cannot keep a continuously running collection within that amount.

A budget alert warns; it does not automatically stop spending. Notifications can arrive after charges accumulate. For this one-day lab, the user chose to skip budget setup. Keep the dataset small, delay vector-store creation, and delete resources after evidence collection the same day.

Sources: [OpenSearch pricing](https://aws.amazon.com/opensearch-service/pricing/), [Bedrock pricing](https://aws.amazon.com/bedrock/pricing/), [S3 pricing](https://aws.amazon.com/s3/pricing/), [AWS Budgets](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html).

## 🧠 Learning depth

**🧹 Cleanup is mandatory:** Collect evidence, then remove all project-created AWS resources and project-only permissions/data. Verify deletion and delayed billing before completion; preserve unrelated shared resources.

- **Understand well:** identity versus permissions, least privilege, idle costs, budget alerts.
- **Basic awareness:** service limits and model availability.

## 🎤 Interview FAQ

**1. Does STS success prove Bedrock access?** No; it verifies identity, not permission to use Bedrock.

**2. Why separate inspection and deployment profiles?** Inspection needs fewer permissions and cannot make deployment changes.

**3. Does listing a model prove it can be invoked?** No; invocation permissions and model access must also be checked.

**4. Can an idle chatbot cost money?** Yes; retained storage and some vector-store compute configurations remain billable.

**5. Does a budget alert cap spending?** No; it notifies you and may be delayed.
