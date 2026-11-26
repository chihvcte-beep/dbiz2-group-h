# ADR-002: Send reader OTP without a separate external email service

| Field | Value |
|---|---|
| Status | Proposed |
| Date | 2026-11-26 |

## Context

Reader sign-in uses a one-time password (OTP) sent to the reader's registered email address. The Context Diagram and AD-UC-11 show the OTP email going to the Reader without a separate external email-service participant. The architecture must preserve this agreed system boundary while avoiding an unsupported choice of email-delivery technology.

## Decision

Do not include a separate external email service as a system participant. Keep the Context Diagram and AD-UC-11 unchanged: the Library Core System sends the OTP to the Reader's email inbox.

**Decision source:** `docs/project/decision-index.md`, Inputs check 2 / AD-UC-11 Q2 (2026-11-04). The corresponding architecture mapping is in `docs/architecture/system-architecture.md`, §§3 and 6.

The technical email-delivery mechanism is not decided by this ADR. It remains an implementation choice to be resolved later; no email provider, SMTP server or delivery technology is selected here.

## Consequences

The system boundary and diagrams do not depend on a separately modelled external email-service component. The reader sign-in flow must handle code-send failure as required by FR-04-16. The implementation team must resolve the delivery mechanism separately without changing the recorded system-boundary decision.
