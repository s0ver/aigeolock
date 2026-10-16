# AIGeoLock

**A secure, modular LLM gateway with geo-aware routing through VPN tunnels.**

AIGeoLock is an open-source project written in Rust. Its goal is to provide a secure, extensible gateway for accessing LLM providers through controlled network tunnels.

The project is being developed incrementally, with a focus on modular architecture, original code, and verifiable security properties.

> **Status: Early development — design and initial implementation pending.**
>
> AIGeoLock is not yet ready for production use.

## Goals

- **Provider-independent core.** Support multiple LLM providers through modular adapters.
- **Protocol-independent networking architecture.** Support multiple tunnel backends through well-defined interfaces.
- **Fail-closed security.** Prevent requests from silently falling back to an unprotected direct connection when the required tunnel is unavailable.
- **Geo-aware routing.** Route requests through configured network endpoints according to explicit policies.
- **Windows-first development.** Begin with Windows and Microsoft SSTP.
- **Incremental implementation.** Start with one LLM provider and one tunnel protocol, then expand without redesigning the core.
- **Original code.** Develop AIGeoLock's implementation independently, using documented standards and carefully reviewed third-party dependencies.

## Initial scope

The first planned integration targets are:

- **Platform:** Windows
- **LLM provider:** OpenRouter
- **Tunnel protocol:** Microsoft Secure Socket Tunneling Protocol (SSTP)
- **Implementation language:** Rust

These are initial development targets, not yet implemented or verified capabilities.

## Architecture

The planned architecture separates the following responsibilities:

- **LLM Gateway** — accepts client requests and exposes a consistent API.
- **Provider adapters** — translate between the gateway's internal model and provider-specific APIs.
- **Core routing engine** — applies routing policies and manages request flow.
- **Tunnel backends** — establish and monitor protected network connections.
- **Security enforcement** — ensures that requests requiring a protected route are blocked when that route cannot be guaranteed.

The core should depend on stable internal interfaces rather than specific providers or tunnel implementations.

## Security principles

Security is a design requirement, not a feature to add later.

- Fail closed when a protected route is unavailable.
- Never silently fall back to direct connections.
- Avoid exposing API keys, credentials, or sensitive request data in logs.
- Audit dependencies, licenses, and known vulnerabilities.
- Test failure and recovery scenarios, not only successful connections.
- Document platform-specific limitations and required privileges.

The actual guarantees will be documented and tested as implementation progresses.

## Development approach

AIGeoLock follows an incremental, AI-assisted development workflow:

1. Define a small, testable task.
2. Implement the minimum necessary change.
3. Run automated tests and review the code.
4. Update documentation and record architectural decisions.
5. Move to the next task only when the current one is understood and verified.

AI-generated code must be reviewed and tested before it is accepted.

## Licensing and third-party code

AIGeoLock is licensed under Apache-2.0.

The project aims to keep its own implementation original. Third-party libraries and tools may be used where appropriate, subject to license compatibility, security review, and clear attribution.

## Project status

The immediate priority is to define the architecture and threat model, establish the core interfaces, and validate the first protected request path.

No production security guarantees are made at this stage.

## Contributing

Contributions, design discussions, bug reports, and security reviews will be welcome as the project matures.

Please use GitHub Issues to discuss proposed changes before undertaking substantial implementation work.
