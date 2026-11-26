# ADR-001: Use one web app for Readers and On-site Staff

| Field | Value |
|---|---|
| Status | Proposed |
| Date | 2026-11-26 |

## Context

The Library Core System serves two user groups: Readers and On-site Staff. They use different screens and perform different tasks, but both interfaces belong to the same Library Core System. The logical architecture needs to show how these interfaces are organized without introducing a second application or treating the staff interface as a separate product.

## Decision

Use one web app in the Presentation layer to provide both Reader screens and Staff screens. The web app communicates with the Backend API, while the system's business functions remain separate logical responsibilities behind that API.

**Decision source:** `docs/architecture/system-architecture.md`, §3 Physical design and §4 Decisions (the row “One web app serving Reader and On-site Staff screens; separate backend functions”). The Decision Index does not assign this architecture-design decision a separate D-ID; no D-ID is claimed for it.

## Consequences

The architecture and system diagrams show one web app serving both user groups. Reader and Staff screens may have different layouts and access rules, while the backend enforces the appropriate authentication, session and role checks. This decision does not select a frontend framework, programming language, hosting platform or deployment topology.
