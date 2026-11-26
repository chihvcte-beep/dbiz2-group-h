# ADR-004: Share one QR code across all copies of a book title

| Field | Value |
|---|---|
| Status | Proposed |
| Date | 2026-11-26 |

## Context

A book title can have more than one physical copy, and those copies may be located on different shelves. The QR-label process therefore needs a consistent identity rule that avoids creating a separate QR code for every physical copy.

## Decision

Generate one unique QR code linked to each book title. All physical copies of the same title share that code; staff reprint the existing code when another label is needed. A reprinted label contains the QR code and title but no shelf location, because copies may be stored on different shelves.

**Decision source:** `docs/project/decision-index.md`, D40 (23/11/2026), which refines D4 and D13; FR-02-07 and FR-02-25. The architecture mapping is in `docs/architecture/system-architecture.md`, §§1, 3.1 and 6.

## Consequences

QR identity is maintained at book-title level rather than physical-copy level. The label-generation and reprint flows must reuse the title's existing QR code. Reprint confirmation records the required audit event but does not change the book's label-printed status, as specified by D40 and the related requirements.
