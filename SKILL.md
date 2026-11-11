---
name: personal-dev-standard
description: Apply the user's personal engineering standards and accumulated lessons when generating or reviewing code, designing architecture or APIs, or developing ArkTS, TK, React Native, automation, agent, and RAG projects.
---

# Personal Dev Standard

Use the shared knowledge base in this repository. Resolve the following paths relative to this `SKILL.md`, not the current working directory:

- Read [coding standards](spec/coding-standard.md) for code and output conventions.
- Read [architecture principles](spec/arch-principles.md) when architecture or module boundaries are relevant.
- Check [pit notes](spec/pit-notes.md) for lessons applicable to the task; surface relevant risks and mitigations.
- For HarmonyOS native ArkTS / ArkUI work, read [Harmony rules](spec/harmony.md).
- For TK work, read [TK rules](spec/tk.md).
- For KRN / React Native bundle work, read [KRN rules](spec/krn.md).
- For cross-platform or container integration work, read the rules for every involved side and check the boundary contract. Identify the stack from the actual project when the name is ambiguous.
- Use the [document template](spec/doc-template.md) when writing a technical design or API document, adapting it to the task.

Explicit user instructions and project-specific conventions take precedence. When a reusable lesson is identified and the user requests that it be recorded, update the appropriate shared spec with its context and tradeoffs.
