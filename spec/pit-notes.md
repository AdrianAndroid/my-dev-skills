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
