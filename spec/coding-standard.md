# Coding Standard

Applicable stacks: Rust / C++ / Kotlin KMP / TypeScript (Node) / ArkTS / React Native / TK projects / GDScript

## General expectation for AI

- Assume familiarity with the listed stacks; do not explain basic syntax or trivial APIs.
- Prefer complete runnable code to fragmented pseudocode. Do not add a demo or main entry unless requested.
- When comparing solutions, consider maintainability, performance, dependency cost, known risks and deployment overhead as relevant.
- Check `pit-notes.md` for applicable known pitfalls and explain the risk and mitigation when relevant.
- Keep Markdown concise, without redundant decorations, separators or emojis.

## Naming rules

- Rust: snake_case variables and functions; PascalCase structs, enums and traits; UPPER_SNAKE_CASE constants.
- C++: camelCase variables; PascalCase classes and structs; MACRO_UPPER; snake_case filenames.
- Kotlin / KMP: camelCase variables and functions; PascalCase classes; UPPER_SNAKE_CASE constants.
- TypeScript: camelCase variables and functions; PascalCase types and classes; kebab-case filenames.
- ArkTS: camelCase variables and functions; PascalCase types, classes and components; follow the project’s ArkUI conventions.
- React Native: follow the project’s TypeScript or JavaScript conventions; use PascalCase for components and camelCase for variables and functions.
- TK projects: follow the project’s established language, framework and naming conventions.
- GDScript: snake_case variables; PascalCase classes.

Follow established project conventions where they differ.

## Comments

Explain why, constraints and side effects rather than repeating the code. Document non-obvious algorithms, unsafe blocks and async race conditions. Avoid redundant comments on straightforward business code.

## Error handling

- Rust: prefer Result/Option; avoid unwrap/expect in main business paths; attach context to errors.
- C++: prefer error codes or expected-style results; avoid exceptions for normal business control flow.
- TypeScript: wrap errors explicitly and avoid naked rejections.
- Do not silently swallow errors; log or propagate them as appropriate.

## Engineering practice rules

1. Before implementing new logic, look for and reuse relevant existing code. Avoid duplicating functionality.
2. Add a corresponding log for every if-else branch. Keep logs concise and necessary; avoid complex or expensive logging that affects runtime performance.
3. When adding new code alongside legacy code, wrap the new path in a feature toggle or switch to distinguish it from the old path.
4. Refine new code carefully during implementation. Avoid accumulating quick-and-dirty hacks and technical debt.

## Imports and includes

Group standard library, stable third-party SDKs, and internal project modules separately, unless project conventions differ.

## Code size

Aim for functions of at most 80 lines and nesting depth of at most four; split when it improves clarity. Extract magic numbers as named constants and explain their meaning when needed.

## Default project layout

- Rust: standard Cargo layout, with domain / infra / api / utils layers.
- Node TypeScript: `src/api`, `src/domain`, `src/infra`, `src/utils`, `tests`.
- Godot: `res/scene`, `res/script`, `res/asset`, `res/config`, split by module.
- C++: `src`, `include`, `tests`, `cmake`.

## Mobile project considerations

- ArkTS: respect the project’s HarmonyOS and ArkUI versions, lifecycle, state management and platform API constraints.
- React Native: consider supported React Native and platform versions, navigation, native module compatibility and iOS/Android behavior when relevant.
- TK projects: inspect the existing project and its documented conventions before choosing dependencies, structure or platform-specific APIs.
