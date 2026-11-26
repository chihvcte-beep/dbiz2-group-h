# ADR-006: Keep library integration read-only and synchronise data daily

| Field | Value |
|---|---|
| Status | Proposed |
| Date | 2026-11-26 |

## Context

The Library Core System relies on information owned by the Library Internal System, including catalogue records, access formats, shelf placement, floor and room data, loans, and account/role information. The system also needs an agreed operational process for library-side changes and a defined use case for scheduled imports.

## Decision

The Library Core System reads the relevant information from the Library Internal System and does not write data back to it. The Library Internal System remains the source of each book's access format. The library agrees to add the new links to its existing OPAC pages. Library staff inform the team when a room is added, renamed or removed, and manually monitor errors and availability after release.

Represent the scheduled import as **UC-15: Sync data from the library internal system**, started by time. The architecture specifies a daily sync at 02:00. The sync covers catalogue, placement/layout and loan data; it retains the last successful data and retries failed imports as required by FR-04-11.

**Decision sources:** `docs/project/decision-index.md`, D47 and D48 (23/11/2026). D47 records the library's integration and operational responsibilities; D48 establishes UC-15 as the time-triggered daily-sync use case. The architecture mapping is in `docs/architecture/system-architecture.md`, §§3, 5, 6 and 7.

## Consequences

The Library Internal System remains the source of truth for the data it owns, and the Library Core System performs read-only integration. The architecture includes a scheduled daily sync represented by UC-15 and its related activity and sequence diagrams. Release 1 relies on library staff for the agreed manual monitoring; automatic tracking and alerts are not introduced by this ADR.

The technical method for reading data from the Library Internal System (for example, an export, file or interface) remains undecided under `system-architecture.md` §8. This ADR does not select that method. The privacy notice and retention period for the anonymous read log also remain open under D47 and are not decided here.
