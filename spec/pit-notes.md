# Pit Notes | Tech Selection & Lessons Learned

## Entry template

- **Scenario**:
- **Problem / requirement**:
- **Tried approaches**:
- **Pitfall & side effect**:
- **Conclusion & practice**:
- **Reference (optional)**:

## Playwright / Puppeteer browser automation

- **Scenario**: SPA asynchronous rendering, unstable selectors and intermittent timeouts.
- **Tried approaches**: fixed sleeps and waiting for selectors or conditions.
- **Pitfall & side effect**: fixed sleeps vary with machine speed; an element in the DOM is not necessarily visible; iframe context can be overlooked.
- **Conclusion & practice**: wait for a meaningful condition such as visibility, use a reusable wait helper when useful, and explicitly handle iframe context. Use the API appropriate to the browser library in use.

## Feature-gated integration into existing flows

- **Scenario**: Introduce a new implementation into an existing entry point while retaining the old behavior as a fallback.
- **Problem / requirement**: Keep the existing path easy to review and preserve its behavior when the feature switch is off or the new implementation cannot start.
- **Pitfall & side effect**: Moving or rewriting the old path to accommodate the new branch increases the diff and can subtly change state, arguments, logging, or fallback behavior. Asynchronous failure may occur after mutable state has changed.
- **Conclusion & practice**: Prefer a switch-guarded new branch before the existing code; return only when the new implementation takes responsibility. Leave the old statements in place whenever practical. Capture the original arguments needed by asynchronous failure callbacks, and ensure fallback executes once without re-entering the enabled new path. A small duplication of the old invocation may be reasonable to preserve the old branch and its captured arguments; extract shared code only when it improves clarity without changing behavior. Check the switch-off, immediate failure, asynchronous failure, and successful paths.

## Serializing nullable values across platforms

- **Scenario**: Aligning a serialized parameter and its fallback with an existing platform implementation.
- **Pitfall**: Confusing a null input with a null serialization result, the literal string `"null"`, an empty string, or an omitted field. Replacing an explicit empty-string fallback with `"null"` changes the contract.
- **Practice**: Follow the reference operation order: inspect the actual serializer call, the value it returns, and the fallback applied to that return value. A reference expression that substitutes `""` when the serializer returns null requires that same fallback; it does not by itself establish what the serializer returns for a null input. Verify the configured serializer and compare null, missing and representative object inputs, including the final encoded and decoded parameter, before claiming equivalent behavior. Do not infer production behavior from a different serializer or an unverified default.

## Gate a new initialization call at the existing entry point

- **Scenario**: A requirement adds a new initialization call to an existing startup or lifecycle method and already has a feature switch.
- **Practice**: Put the switch around the newly added call at that existing entry point, leaving neighboring original initialization unchanged. Do not repeat the same gate inside the new `init()` solely to protect that call; retain privacy checks and independent feature-specific guards. Inspect other callers and deferred callbacks before removing a gate so existing behavior and authorization remain intact. Respect module dependency direction: if an API module cannot import a switch utility from its implementation module, use the existing available configuration API or an appropriate shared abstraction; keep the switch key and default consistent and report any duplication.

## Building route query parameters

- **Scenario**: A route or deep link has multiple parameters, including nested URLs or JSON.
- **Problem / requirement**: Keep parameters readable and maintain the existing caller-to-container encoding contract.
- **Pitfall & side effect**: Manual concatenation makes separators and escaping easy to miss. Passing pre-encoded values to a parameter builder can double-encode them; raw query suffixes and repeated keys can also have special semantics. Different URI parsers may decode `+` and percent escapes differently.
- **Conclusion & practice**: Prefer a URL query builder already used by the project (for Harmony ArkTS, consider `url.URLParams`); provide raw values and let it encode once. Treat any already-encoded suffix according to its existing contract. Compare decoded old and new parameters with representative nested URLs, non-ASCII text, spaces, plus signs, ampersands, percent escapes, empty values, and duplicate keys where applicable. Verify with the actual target router and device; a generic runtime comparison alone does not establish platform behavior.

## Aligning a cross-platform implementation with a reference project

- **Scenario**: The user asks a Harmony, TK, or KRN implementation to match an Android or other existing implementation as closely as practical.
- **Pitfall & side effect**: Matching class names or adding a thin forwarding layer while retaining different responsibilities can make the code appear aligned even though the base class, lifecycle, callbacks, fallback, or call graph differ. Compilation alone does not establish architecture or behavioral equivalence.
- **Conclusion & practice**: Before implementation, inspect the reference and map directories, class names, ownership, public methods, models, call flow, listener contracts, cleanup, and fallback to the target. Implement the requested in-scope responsibilities rather than only matching names. Adapt platform-specific APIs and honor explicitly excluded features; document any remaining differences and why they remain. Compare against the reference again after implementation and separately report build, runtime, and device verification.

### Complete class-level alignment and verification

When asked to align a class with a reference implementation, treat the class and its in-scope call chain as the unit of work, not just the line the user pointed out. Before editing, compare all already-used fields and their names, types, defaults, serialization, ownership and data sources; also compare constructors, method parameters and return values, callers, listeners, lifecycle and fallback. Check related models and callers so that moving one responsibility does not leave another misaligned.

Resolve all identified in-scope differences as part of the same task without waiting for the user to point out each one. Preserve explicitly excluded features and do not invent unavailable data sources. Classify remaining differences as a necessary platform adaptation, an excluded or unimplemented feature, or an unresolved issue, and explain the reason. After the changes, compare the reference against the target again in both directions; report specific remaining differences and distinguish compilation from behavioral and device verification. Do not claim full alignment based solely on naming, a passing build, or one corrected parameter.

## Native host and KRN adaptation

- **Scenario**: Adapting an existing Android-driven KRN dialog to Harmony with future migration planned.
- **Pitfall & side effect**: A working local default can be mistaken for the Android EVE configuration; changing an established React Native dependency or page rendering condition without evidence can introduce cross-platform changes. A successful build does not prove actual container parameters, lifecycle, network data or device layout.
- **Conclusion & practice**: Trace Android strategy fields, processor selection and KRN initial props before designing the host. Keep Android model names and field nesting for fields actually used; distinguish native strategy style strings from numeric KRN UI styles. Preserve existing KRN code and dependencies unless an evidenced Harmony adaptation is needed. Distinguish prefetch invocation from network requests and cache use, and verify encoding, safe-area sizing and failure fallback on the target device. Keep user-requested temporary switches and diagnostic logs identifiable for later cleanup.

