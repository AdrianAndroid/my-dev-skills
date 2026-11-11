# HarmonyOS native: ArkTS and ArkUI

Apply the shared coding standard and project rules first.

- Follow the repository's ArkTS/ArkUI SDK, module, import, router, and build conventions. Reuse existing container and utility capabilities before introducing dependencies or shared-framework changes.
- For a feature added to an existing entry point, guard new work with the requirement's switch and preserve the original branch and original logs. Keep asynchronous fallback scoped to the originating request; avoid duplicate fallback and stale scene/context.
- Treat type assertions and network model declarations as compile-time assumptions, not runtime validation. Handle platform API errors and async lifecycle changes according to the existing contract.
- For KRN hosting, inspect the actual Harmony container's route handling, sizing and safe-area behavior. Check query encoding and decode behavior on the target router; screen-height parameters alone do not guarantee safe-area coverage.
- Build the affected Harmony module when feasible; device validation is separate from compilation. Preserve user-requested temporary test switches and clearly report their status.
- When the user requests strict Android alignment, put models in the corresponding model directory and preserve Android model names, field names, types, ownership, and JSON nesting. Add fields when actually used; do not mix fields from distinct Android models into an invented combined model or represent KRN-only fields as Android native model fields. Clearly identify temporary local defaults and unimplemented fields.
