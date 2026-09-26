# 📍 Project Progress

**🟡 Now:** Step 1 — finish understanding checks; diagram ready.  
**⏭️ Next:** Step 2 — AWS access and costs.  
**Hands-on:** No project resources or results verified yet.

## 🚦 Rules

- **Explain → build → you run → check → record.**
- Check each step only after **all sub-checks pass**, including the 🎤 learning/interview questions. Then start the next step.
- Before cloud work: review official AWS guidance and explain commands, expected results, and costs. You execute deployment commands manually.
- Add detailed topic guides when needed. Record actual results, not assumptions.
- Cleanup is allowed anytime to stop charges.

## 🔐 AWS settings

| Setting | Value |
| --- | --- |
| Preferred Region | `us-east-1` |
| Approach | AWS CLI command-first |
| Access | Identity checks passed per your report; permissions unverified |

Account and profile details are kept in the ignored local file `.local/aws-settings.md`. Use the read-only profile for inspection. Never publish secrets, credentials, or classified information.

## 🪜 Checklist

Depth: **🧠 Understand well** · **💡 Concept only** · **👀 Basic awareness**

- [ ] **1. 🟡 Understand the architecture**
  - Topics: 🧠 document and question flows, service roles; 💡 vectors.
  - [ ] Read [Architecture](docs/01_architecture.md); explain both flows and the chatbot's scope.
  - [x] Add colorful Mermaid diagrams directly in the architecture document; label planned parts.
  - [ ] 🎤 Where does chunking run? Why sync? How do Titan and the chat model differ? Do citations prove accuracy?
  - [ ] 📝 Record reviewed answers and the diagram link.

- [ ] **2. 🔐 Verify AWS access and costs**
  - Topics: 🧠 Region, permissions, charges; 👀 service limits.
  - [ ] Verify service/model availability in `us-east-1` and required profile permissions.
  - [ ] Review costs and cleanup; configure and check the agreed cost alert.
  - [ ] 🎤 What costs money while idle? Does an alert stop spending? Why limit permissions?
  - [ ] 📝 Record access results, cost estimates, and alert verification.

- [ ] **3. 📄 Prepare documents and S3**
  - Topics: 🧠 buckets, files, prefixes (folder-like paths), source quality.
  - [ ] Select approved runbooks without secrets; prepare questions, expected answers, and an unsupported question.
  - [ ] Configure S3, upload documents, and verify contents, locations, and access.
  - [ ] 🎤 Why do accurate runbooks and environment labels matter?
  - [ ] 📝 Record uploaded files, results, and the topic link.

- [ ] **4. ⚙️ Configure the Knowledge Base**
  - Topics: 🧠 S3 connection, chunk size/overlap, Titan, OpenSearch, permissions; 💡 other chunking options.
  - [ ] Choose and explain chunking settings, embedding settings, and the chat model.
  - [ ] Configure the Knowledge Base, S3 connection, OpenSearch Serverless, and access rules.
  - [ ] Verify settings and access; update the diagram to show configured parts.
  - [ ] 🎤 Who splits, embeds, and stores text? How do chunk size and overlap affect retrieval?
  - [ ] 📝 Record settings, resource IDs, and the topic link—no secrets.

- [ ] **5. 🔎 Sync and check passages**
  - Topics: 🧠 sync, retrieved passages, sources, Top-K (number of results requested).
  - [ ] Run sync; check completion and resolve failures.
  - [ ] Test prepared questions; verify passages include the right commands, warnings, and environment.
  - [ ] 🎤 Does successful sync guarantee useful results? What does Top-K control?
  - [ ] 📝 Record passages, sources, fixes, and the topic link.

- [ ] **6. 💬 Check generated answers**
  - Topics: 🧠 retrieval versus generation, evidence, citations, missing information.
  - [ ] Compare generated answers with expected answers and cited passages.
  - [ ] Test missing evidence; verify the answer acknowledges the gap. Resolve failed checks.
  - [ ] 🎤 How do you distinguish poor retrieval from poor answer generation?
  - [ ] 📝 Record expected versus actual answers and the topic link.

- [ ] **7. 🖥️ Build the chatbot**
  - Topics: 🧠 app flow, AWS calls, sources, errors, safe credentials.
  - [ ] Build the simple chatbot with learning comments and a linked code guide.
  - [ ] Run it; check answers, sources, missing evidence, and an error case. Keep credentials out of code and output.
  - [ ] 🎤 Trace a question through the app. How does it access AWS without keys in code?
  - [ ] 📝 Record results; update the diagram and code guide.

- [ ] **8. 🛡️ Demonstrate a guardrail**
  - Topics: 🧠 one content check and its limits.
  - [ ] Configure one control; test allowed and blocked requests and displayed responses.
  - [ ] 🎤 Why doesn't a guardrail replace permissions or guarantee correct answers?
  - [ ] 📝 Record settings, results, limits, and the topic link.

- [ ] **9. ♻️ Test document changes**
  - Topics: 🧠 updates, deletion, sync, outdated passages.
  - [ ] Record a baseline; update a runbook, sync, and verify the revised passage and answer.
  - [ ] Review deletion settings; delete a sample source, sync, and verify old passages disappear.
  - [ ] 🎤 Why isn't changing or deleting an S3 file enough to prove answers are current?
  - [ ] 📝 Record before/after results and the topic link.

- [ ] **10. 📊 Monitor and test load**
  - Topics: 🧠 response time, errors, request counts; 👀 limits and scaling.
  - [ ] Enable monitoring; verify a sample request is recorded.
  - [ ] Set request/concurrency limits, duration, cost allowance, and stop conditions; run the small test.
  - [ ] Review measurements and investigate failures.
  - [ ] 🎤 What could slow requests down? Why doesn't this test prove large-scale performance?
  - [ ] 📝 Record measurements, test limits, and the topic link. Separate assumptions from results.

- [ ] **11. 🧹 Clean up and review**
  - Topics: 🧠 resource removal, remaining charges, interview evidence.
  - [ ] Review and remove lab resources and unwanted stored data/logs.
  - [ ] Verify removal and remaining charges; account for billing delays and record retained items or follow-ups.
  - [ ] 🎤 Why isn't deleting the chatbot enough to stop costs? Explain one failure, one design choice, and our test limits.
  - [ ] 📝 Save final results and links; mark the diagram as cleaned up.

## 📝 Verified results

No full step verified yet.

- **Local setup:** NVM 2.0.0, Node 24.21.0, and npm 11.19.0 installed and version-checked.
- **Diagrams:** Mermaid flows are included in [Architecture](docs/01_architecture.md). AWS components remain planned; preview rendering needs your check.
- **Learning:** You explained S3 → chunks → Titan → vector store. Clarification: uploading alone does not start ingestion; run KB sync, then Bedrock applies chunking. Confirm sync and explain why citations do not prove accuracy; remaining Step 1 checks stay open.

Use one short entry per completed step:

**Date · Step · Topic link · Expected → actual result · Learning check · Follow-ups**
