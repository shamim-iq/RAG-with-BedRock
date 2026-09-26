# Learning conventions

- Keep this a straightforward DevOps learning project.
- Work incrementally: explain → implement → user executes → check → document.
- Explain commands, settings, expected results, and costs before cloud activities.
- Maintain numbered AWS CLI steps in `docs/03_cli_execution.md`, with a short purpose, cost, and expected result. Add commands as each topic is reached. Use placeholders such as `<aws-profile>`, `<account-id>`, and `<notification-email>` in shared instructions; keep actual values and execution evidence local-only.
- Ask occasional short understanding questions after meaningful steps.
- Never mark hands-on work complete without observed results.
- Create topic documents as we reach them; avoid filling future topics in advance.
- Use familiar words, concise bullets, DevOps examples, and light emojis.
- Explain necessary terms. Use colorful Mermaid diagrams with text labels and text equivalents.
- End theory documents with `## 🎤 Interview FAQ` and 4–6 short question/answer pairs.
- Separate plans from actual observations. Never claim untested scale.
- Maintain current and next activity in local-only `PROGRESS.md`; create it if missing. Keep it ignored and never commit it.
- Keep code simple: small functions, descriptive names, concise docstrings and intent comments.
- Include a short data flow at the top of pipeline files.
- Highlight complete important Python sections with these exact markers, with a short what/why explanation above:
  `# You should understand ----------------------------------------------------->`
  `# -------------------------------------------------------------------------->`
- Leave boilerplate unmarked. Explain parameters and units.
- Add a linked code file guide when code is introduced and maintain it as files change.
- Depth labels: Understand well, Concept only, Basic awareness.
- Check official AWS documentation before writing service-specific setup steps.
- **Hard rule:** Never publish secrets, credentials, or classified information to any remote. Keep private project settings in ignored `.local/` files; keep credentials in the existing local credential store and never display them.
- Before every commit/push, review staged files and outgoing history for sensitive information. Never force-add ignored private files. Record only sanitized observations in shared docs.
- Keep AWS profile policy JSON files in ignored `.local/`; read `.local/POLICIES.md` for scope and application notes.
- Codex uses only the read-only AWS profile for account operations. The user executes all deployment, model invocation, ingestion, permission changes, and cleanup using the deployment profile. Never switch profiles to bypass denied inspection.
- **Mandatory cleanup:** After verification and evidence collection, remove every AWS resource created for this project, including project-only data, logs, roles, policies, and alerts. Track resources locally as they are created. Preserve unrelated pre-existing/shared resources; remove only this project's additions. Explain cleanup commands for the user to execute manually, verify deletion and any delayed billing, and never mark the project complete while cleanup remains unresolved.

## Architecture diagrams

- Use Mermaid directly inside Markdown for architecture and workflows; no separate diagram directory or HTML artifacts.
- Use colors, grouped stages, short labels, and emojis. Keep diagrams static and compatible with Markdown previews.
- Label planned components clearly; update diagrams to match the implemented system.
- Keep diagrams simple, colorful, and readable, with text labels and a short written explanation.
