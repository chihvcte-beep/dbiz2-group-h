# Architecture Decision Records

These ADRs map the six decision rows in `docs/architecture/system-architecture.md` §4.

| ADR | Architecture decision | Decision Index source |
|---|---|---|
| ADR-001 | One web app for Reader and Staff screens | System Architecture §§3–4; no separate D-ID is assigned |
| ADR-002 | OTP email without a separate external email-service participant | AD-UC-11 Q2 / Inputs check 2 |
| ADR-003 | Staff session ends only on explicit sign-out | D7; D36 clarifies an already-ended session |
| ADR-004 | One shared QR code per book title | D40 (refines D4 and D13) |
| ADR-005 | Reader 360px and Staff 1280px supported widths | D44, D45 (supersede D8) |
| ADR-006 | Read-only library integration and daily sync as UC-15 | D47, D48 |

## Status and scope

The records use `Proposed` because `system-architecture.md` v1.3 (26/11/2026) says the ADR files are pending and explicitly warns not to mark them `Accepted` solely because the underlying group decision is recorded. Update status only after the group has reviewed and accepted the ADR records.

These ADRs record agreed architecture decisions; they do not choose implementation technologies that the architecture leaves open. In particular, the OTP delivery mechanism and the technical method for reading Library Internal System data remain undecided.
