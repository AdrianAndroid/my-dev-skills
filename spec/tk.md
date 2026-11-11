# TK projects

Apply the shared coding standard and project rules first.

- Identify the actual TK framework, language version, project structure and build tool from the repository; do not assume React Native, KRN, ArkUI, or browser APIs are available or interchangeable.
- Reuse the project's existing components, state patterns, navigation, bridge and event APIs. Verify platform support and native/host contracts from local code or documentation before using a capability.
- For cross-end migration or integration, compare the existing implementation's inputs, lifecycle, fallback, rendering, interaction and tracking; preserve behavior unless the task explicitly changes it.
- Run the project's applicable build/type checks when available, and distinguish those checks from runtime and device validation. Avoid adding or changing dependencies without an evidenced need.
