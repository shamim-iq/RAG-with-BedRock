# 🛠️ DevOps Runbook Chatbot — Bedrock RAG Lab

## 🎯 Objective

Build a small chatbot that answers DevOps questions from approved documents. Understand the flow, prove its behaviour, and explain the decisions in interviews.

**RAG (Retrieval-Augmented Generation):** find relevant passages and give them to a chat model as evidence.

## 🧭 Start here

1. Read [Architecture and workflow](docs/01_architecture.md).
2. Try its understanding questions before setup.
3. Follow the [AWS CLI execution sequence](docs/03_cli_execution.md) as each activity is reached.
4. Read [RAG permission layers](docs/06_permissions_explained.md) to understand the service role.

**Status:** 🟡 Sample runbooks uploaded to S3; bucket privacy and encryption verified. Knowledge Base and chatbot setup are pending.

## 🔄 Planned flow

📄 Runbooks → 🪣 S3 → 📥 Knowledge Base sync → ✂️ Chunks → 🔢 Titan embeddings → 🔎 OpenSearch

💬 Question → 🔎 Retrieve passages → 🤖 Chat model → ✅ Answer with sources

## ✅ Scope

- Simple chatbot with source references.
- S3, Bedrock Knowledge Bases, Titan embeddings, and OpenSearch Serverless.
- Clear permissions and one guardrail demonstration.
- Tests for missing evidence, updated documents, and deleted documents.
- Basic monitoring, a controlled load test, scaling explanation, and cleanup.

Reuse existing DevOps sample documents when we reach ingestion. An agent and live Kubernetes access are not required for the initial chatbot.

## 🧪 Learning rhythm

**Understand → implement → you execute → inspect → document.**

Before each activity: explain its purpose, settings, expected result, and cost. After important steps: ask a few short understanding questions. Add topic documents as we reach them, with actual observations beside the steps.

## 🎤 Interview evidence

Show the source behind an answer, demonstrate an update and deletion, explain a failure, and report actual measurements. Production readiness and large-scale performance must be demonstrated, not assumed.
