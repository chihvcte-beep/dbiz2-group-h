# ADR-005: Set separate supported widths for Reader and Staff screens

| Field | Value |
|---|---|
| Status | Proposed |
| Date | 2026-11-26 |

## Context

Readers primarily use the Reader interface on phone-sized screens, while On-site Staff use the Staff interface on library computers. Earlier responsive-width guidance was inconsistent with the final screen specifications and was superseded by separate decisions for the two user groups.

## Decision

Reader screens are designed and supported at 360px; narrower widths are not supported. Staff screens are designed and supported at 1280px; narrower widths are not supported. Do not apply the superseded narrower-width behavior from D8.

**Decision source:** `docs/project/decision-index.md`, D44 and D45 (23/11/2026), which supersede the corresponding parts of D8. The architecture mapping is in `docs/architecture/system-architecture.md`, §7.

## Consequences

Reader screen specifications and wireframes use the 360px design frame. Staff screen specifications and wireframes use the 1280px design frame. The interface is not required to shrink, stack or otherwise adapt below those supported widths. These decisions define supported design widths, not a choice of frontend framework or CSS implementation.
