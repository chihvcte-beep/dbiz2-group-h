# ADR-003: End staff sessions only on explicit sign-out

| Field | Value |
|---|---|
| Status | Proposed |
| Date | 2026-11-26 |

## Context

On-site Staff use protected staff screens to print QR labels and moderate reported reviews. The session rule must be consistent across staff screens and the sign-in/sign-out flow.

## Decision

A staff session has no inactivity time-out. It remains valid until the staff member explicitly chooses «Đăng xuất», which ends the session and opens the staff sign-in screen.

**Decision source:** `docs/project/decision-index.md`, D7 (22/11/2026); FR-04-21. The architecture mapping is in `docs/architecture/system-architecture.md`, §§1, 3.1 and 7.

## Consequences

The architecture must not add automatic staff-session expiry based on inactivity. Staff screens must check that the session is still valid before performing protected actions. If the session has already ended elsewhere, the next staff action follows D36 and returns to the staff sign-in screen; this check is not a time-out. Session storage and revocation implementation remain technical choices and are not specified by this ADR.
