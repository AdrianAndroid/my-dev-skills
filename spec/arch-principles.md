# Architecture Principles & Boundary Rules

## Layering

- **domain**: core business models and rules; does not depend on infrastructure implementations.
- **infra**: implementations for external resources, such as storage, SFTP, browser drivers, third-party SDKs and file IO.
- **api**: entry points, parameter validation, request adaptation, and tool or HTTP interfaces.
- **utils**: pure stateless helpers without business logic.

## Boundary rules

1. Domain does not directly import infrastructure implementations.
2. Define required abstractions in domain; implement them in infra.
3. Agent tool definitions belong in api; execution logic belongs in domain or infra.
4. RAG retrieval implementation belongs in infra; business judgment after retrieval belongs in domain.

Apply these boundaries where the project warrants them; follow a project's existing architecture and explicit requirements when they differ.
