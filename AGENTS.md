# Learning conventions

- Keep this a straightforward DevOps learning project.
- Work incrementally: explain → implement → user executes → check → document.
- Explain commands, settings, expected results, and costs before cloud activities.
- Ask occasional short understanding questions after meaningful steps.
- Never mark hands-on work complete without observed results.
- Create topic documents as we reach them; avoid filling future topics in advance.
- Use familiar words, concise bullets, DevOps examples, and light emojis.
- Explain necessary terms. Use colorful Mermaid diagrams with text labels and text equivalents.
- End theory documents with `## 🎤 Interview FAQ` and 4–6 short question/answer pairs.
- Separate plans from actual observations. Never claim untested scale.
- Maintain current and next activity in PROGRESS.md.
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

## Architecture diagrams

- Use Mermaid directly inside Markdown for architecture and workflows; no separate diagram directory or HTML artifacts.
- Use colors, grouped stages, short labels, and emojis. Keep diagrams static and compatible with Markdown previews.
- Label planned components clearly; update diagrams to match the implemented system.
- Keep diagrams simple, colorful, and readable, with text labels and a short written explanation.
