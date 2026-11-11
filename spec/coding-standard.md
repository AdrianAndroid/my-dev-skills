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
   During AI-assisted development, prioritize comprehensive logging across key flows, branches, state changes, and errors so behavior can be diagnosed. Refine and reduce logs in a later pass while retaining the information needed for troubleshooting; avoid logging sensitive data.
   Mark detailed development-stage logs with a prominent, consistent temporary marker (for example, `TEMP_DEV_LOG`) so they can be found and reviewed for removal or reduction after development.
   Treat the entire requirement as the review scope: compare against the relevant upstream base branch, including all commits and working-tree changes, rather than only the latest commit. Preserve upstream log statements, tags, levels, and contents; do not replace or modify them for diagnostics. Append separate AI troubleshooting logs where needed, retain the agreed filter tag, and mark each temporary log consistently for later removal.
   Keep each temporary diagnostic log statement on a single line, even if it exceeds normal line-length conventions, so it can be found and removed as one complete statement. Preserve the original business code; when a repeated read-only, side-effect-free call is safe, call it separately inside the temporary log instead of extracting a variable that remains after the log is removed.
3. When adding or replacing logic in an existing feature, use a feature toggle or switch to clearly separate the new code from the existing code. Run the new logic when the switch is enabled and preserve the original behavior when it is disabled. Keep the two paths distinct and avoid intermixing them.
   Manage switches in a dedicated switch configuration class, such as `SwitchConfigUtils.ets`. First look for an existing class with the same purpose and reuse it; if none exists, create a new `XXXSwitchConfigUtils.ets` class appropriate to the feature or module.
   Use one shared switch for the same requirement. Unless explicitly requested otherwise, guard all new code developed on the branch for that requirement with that switch.
   This includes new statements or calls inserted into an existing method, even when they do not replace an old branch. For example, guard a newly added prefetch call in `init()` with the requirement's switch, while leaving the existing initialization outside the guard. When the switch is disabled, the added call must not execute.
   Enable newly added switches by default during development. After development is complete, decide the appropriate final default value based on the feature and rollout requirements.
4. Refine new code carefully during implementation. Avoid accumulating quick-and-dirty hacks and technical debt.

## Imports and includes

Group standard library, stable third-party SDKs, and internal project modules separately, unless project conventions differ.

## API URLs

Before adding an API URL or path (for example, `/rest/n/external-touch/head-image/cold-start`), look for an existing centralized URL or endpoint configuration in the project and use it when available. If none exists, extract the URL or path into a clearly named variable or constant rather than embedding it directly in the request logic.

## Method parameters

Unless the user explicitly requests otherwise or the API has a concrete reason, avoid an excessive number of method parameters. Prefer existing domain models and the owning object's established state or data sources; pass cohesive business inputs rather than expanding their individual fields at every layer. Do not invent a combined model, hide dependencies, or change data ownership solely to shorten a signature. When aligning with a reference implementation, inspect its parameter and data ownership first, and preserve lifecycle and behavior when adapting it.

## Multiline conditions

For a multiline condition joined with `||`, prefer placing `||` at the start of continuation lines so each alternative is easy to scan. Follow an explicit project formatter or established local convention when it requires a different style; do not alter the condition's behavior when reformatting.

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
