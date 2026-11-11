# KRN / React Native bundles

Apply the shared coding standard and project rules first.

- Treat the existing bundle and Android behavior as the baseline when adapting to Harmony. Change shared business rendering, dependencies, configuration, or the React Native runtime only when the need is supported by evidence; isolate platform-specific behavior where appropriate.
- Verify the actual bundle ID, registered component/app key, host container route, initial props, and bridge/event contract on both sides. Check event subscriptions, cleanup, instance isolation and failure fallback when relevant.
- Trace parameter encoding and decoding end to end, including nested URLs, JSON and Base64 variants; do not double-encode. Do not infer runtime validation from TypeScript types or fix a compile error by assuming an unverified runtime value.
- Distinguish bundle generation, type checking, running-device bundle selection, and visual/device verification. A displayed page does not establish that the latest build or type check succeeded.
- Follow the bundle's React/React Native and TypeScript conventions; check actual native module support and platform-specific layout/safe-area behavior before choosing an API.
