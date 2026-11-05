# my-dev-skills

Personal development skill set, coding standards and engineering experience base. Platform-agnostic, built for AI-assisted development.

> Current adapter: Codex Skill. Future adapters can include Cursor, Windsurf, Claude and local RAG.

## Structure

- `spec/`: shared, tool-independent knowledge
  - `coding-standard.md`: code style, naming, error handling and output conventions
  - `arch-principles.md`: architecture layers and module boundaries
  - `pit-notes.md`: pitfalls, technical decisions and lessons from practice
  - `doc-template.md`: technical design and API document template
- `adapters/codex/SKILL.md`: Codex skill entry point

## Usage with Codex

Keep the repository together so the adapter can read the shared `spec/` files. Add `adapters/codex/` as a local skill folder in Codex, or configure a skill installation that preserves its relative position within this repository. Invoke it explicitly with `$personal-dev-standard`; it can also be selected automatically for relevant development tasks.

## Accumulating experience

1. Correct an output when it misses an expectation, and identify the reusable lesson.
2. Update the relevant file under `spec/`: coding and output conventions, architecture boundaries, or pitfalls and tradeoffs. Record context and evidence for lessons so they are not applied outside their valid scope.
3. Review and commit the change. Adapters that reference these files inherit the updated knowledge.

## Covered stack

Rust, C++, Kotlin KMP, TypeScript (Node.js), ArkTS, TK projects, React Native, Godot 3D, browser automation, and RAG and agent development.
