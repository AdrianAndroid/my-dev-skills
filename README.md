# my-dev-skills

Personal development skill set, coding standards and engineering experience base for AI-assisted development.

## Structure

- `spec/`: shared, tool-independent knowledge
  - `coding-standard.md`: code style, naming, error handling and output conventions
  - `arch-principles.md`: architecture layers and module boundaries
  - `pit-notes.md`: pitfalls, technical decisions and lessons from practice
  - `doc-template.md`: technical design and API document template
- `SKILL.md`: skill entry point

## Usage with Codex

Keep the repository together so the skill can read the `spec/` files. Install the repository as a local skill folder in Codex. Invoke it explicitly with `$personal-dev-standard`; it can also be selected automatically for relevant development tasks.

## Accumulating experience

1. Correct an output when it misses an expectation, and identify the reusable lesson.
2. Update the relevant file under `spec/`: coding and output conventions, architecture boundaries, or pitfalls and tradeoffs. Record context and evidence for lessons so they are not applied outside their valid scope.
3. Review and commit the change. The skill uses the updated knowledge.

## Covered stack

Rust, C++, Kotlin KMP, TypeScript (Node.js), ArkTS, TK projects, React Native, Godot 3D, browser automation, and RAG and agent development.
