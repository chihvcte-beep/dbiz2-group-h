# Activity Diagram: AD-UC-15 Sync data from the library internal system

| Field | Value |
|---|---|
| AD ID | AD-UC-15 |
| Use case | UC-15 Sync data from the library internal system |
| Feature | F-04 Platform, Access & Operations |
| Primary actor | None: the use case is started by time (daily sync time). The Library Internal System supplies the data |
| Lanes | Library Core System · Library Internal System |
| Inputs (L3-L5) | Context Diagram (Library Internal System flows "Book catalog & availability", "Shelf placement, floors & rooms", "Borrow/return records") · Sequence: [SD-UC-15](../use_case/sd_uc_15.md) · W0 Table 1 (UC-15), Table 4 (Book catalogue, Book placement & library layout, Reader loan records: EIF) · W1 rows FR-04-09, FR-04-10, FR-04-11, FR-04-12, FR-01-05 |
| Trigger | Time event: the daily sync time is reached (02:00) |
| Preconditions | The connection to the Library Internal System is set up. The digital floor plan exists and its rooms carry the room codes of the internal system (FR-01-04). |
| Success end state | The catalogue, shelf codes, floors and rooms and the loan records of library card accounts are imported without writing back; room codes that do not match the floor plan are reported; an audit entry is written. QR generation (AD-UC-10 `t1`) and reading-history entries from new loans (AD-UC-07 `t1`) can start. |
| Failure end state | The internal system does not answer or returns an error three retries in a row: the last successful data is kept and every error is in the audit log. |
| FRs covered | FR-04-09, FR-04-10, FR-04-11, FR-04-12, FR-01-05 |
| Business rules applied | The platform only reads from the Library Internal System and never writes back (W0 Table 4; FR-04-09, FR-04-10). A failed run keeps the last successful data and is retried up to 3 times (FR-04-11). Every sync run writes an audit entry (FR-04-12). Library staff tell the team when a room is added, renamed or removed (D47); FR-01-05 reports the codes that no longer match. |
| Version / status | v1.0 · Draft |
| Author | Owner A (F-04) |

## 1. Diagram

Notation follows the DBIZ2 activity profile and the GeeksforGeeks notation sheet the team uses.
Rendered with `swimlane-beta`, which needs Mermaid 11.16 or later.

```mermaid
---
config:
  theme: base
  themeVariables:
    primaryColor: "#d5e8d4"
    primaryBorderColor: "#333333"
    lineColor: "#000000"
    clusterBkg: "#ffffff"
    clusterBorder: "#333333"
---
swimlane-beta TB
  subgraph SYS["Library Core System"]
    t1@{ shape: hourglass }
    m0{" "}
    s1("Request the catalogue, shelf codes, floors and rooms (FR-04-09)")
    d1{"Was the data returned without error?"}
    s2("Import the catalogue, shelf codes, floors and rooms<br/>without writing back (FR-04-09)")
    s3("Request the loan records of library card accounts (FR-04-10)")
    d2{"Were the loan records returned without error?"}
    s4("Import the loan records without writing back (FR-04-10)")
    s5("Report room codes that do not match<br/>the floor plan (FR-01-05)")
    s6("Write an audit entry for the sync run (FR-04-12)")
    mE{" "}
    s7("Keep the last successful data and write<br/>the error to the audit log (FR-04-11)")
    d3{"Fewer than 3 retries for this run?"}
    stop1@{ shape: fr-circ }
    stop2@{ shape: fr-circ }
  end
  subgraph INT["Library Internal System"]
    i1("Return the catalogue, shelf codes, floors and rooms (FR-04-09)")
    i2("Return the loan records (FR-04-10)")
  end

  t1 -->|"Daily sync time reached (02:00)"| m0 --> s1 --> i1 --> d1
  d1 -->|"[Yes]"| s2 --> s3 --> i2 --> d2
  d1 -->|"[No]"| mE
  d2 -->|"[Yes]"| s4 --> s5 --> s6 --> stop1
  d2 -->|"[No]"| mE
  mE --> s7 --> d3
  d3 -->|"[Yes]"| m0
  d3 -->|"[No]"| stop2
```

Reading notes:

- No person starts this use case. The hourglass `t1` is a **time event**; the time expression is
  written on its outgoing arrow. There is no Reader or On-site Staff lane, so no action needs a screen.
- `m0` is the merge a retried run comes back through; `mE` gathers the two failures before `s7`.
- The two timed steps drawn in other diagrams start when this run has finished: QR codes for new
  physical books (AD-UC-10 `t1`, FR-02-07) and reading-history entries from new loans (AD-UC-07 `t1`,
  FR-03-03).
- This diagram closes Inputs check 3 and L8-20 (D48). The Use Case Diagram PDF still has to show UC-15.

## 2. Node trace

| Node | Kind | Text | Traces to |
|---|---|---|---|
| t1 | Time event | Daily sync time reached (02:00) | FR-04-09 |
| s1 | Action | Request the catalogue, shelf codes, floors and rooms | FR-04-09 |
| i1 | Action (Library Internal System) | Return the catalogue, shelf codes, floors and rooms | FR-04-09 |
| d1 | Decision | Was the data returned without error? | FR-04-11 |
| s2 | Action | Import the catalogue, shelf codes, floors and rooms without writing back | FR-04-09 |
| s3 | Action | Request the loan records of library card accounts | FR-04-10 |
| i2 | Action (Library Internal System) | Return the loan records | FR-04-10 |
| d2 | Decision | Were the loan records returned without error? | FR-04-11 |
| s4 | Action | Import the loan records without writing back | FR-04-10 |
| s5 | Action | Report room codes that do not match the floor plan | FR-01-05 |
| s6 | Action | Write an audit entry for the sync run | FR-04-12 |
| s7 | Action | Keep the last successful data and write the error to the audit log | FR-04-11 |
| d3 | Decision | Fewer than 3 retries for this run? | FR-04-11 |

## 3. Branches and acceptance tests

| Branch | Given | When | Then |
|---|---|---|---|
| d1 [Yes] → d2 [Yes] | the internal system has 25 new physical books and 40 new loans | the 02:00 sync runs | both are imported, nothing is written back, and an audit entry "sync run, time" is written |
| s5 | room R-305 exists in the synced layout but not on the floor plan | the sync finishes | R-305 is reported as a room code with no room on the floor plan |
| d1 [No] → d3 [Yes] | the internal system does not answer at 02:00 | the sync runs | the last successful data is kept, the error is logged and the run is retried |
| d2 [No] → d3 [No] | the loan records fail on the first run and on 3 retries | the last retry fails | the last successful loan data is kept, every error is in the audit log and the run stops |

## 4. Object states used

| Object | States in this diagram |
|---|---|
| Book catalogue, Book placement & library layout | Synced (read only; written by `s2` into the platform copy) |
| Reader loan records | Synced (read only; written by `s4` into the platform copy) |
| Audit entry | written by `s6` (sync run) and `s7` (sync error) |

## 5. Screens touched

None: the use case is started by time and has no Reader or On-site Staff lane (screen-list "What is
deliberately not a screen").

## 6. Open questions

None. Decisions: see [decision_index.md](../project/decision_index.md#ad-uc-15).

## 7. Verification log

| Check | Result | By | Date |
|---|---|---|---|
| Every decision has guards on all outgoing flows | Pass (checked by script) | AI assistant | 2026-11-23 |
| No action or decision has two incoming flows without a merge | Pass (checked by script) | AI assistant | 2026-11-23 |
| Every action cites one FR | Pass | AI assistant | 2026-11-23 |
| Every FR of UC-15 appears in the diagram | Pass (FR-04-09, FR-04-10, FR-04-11, FR-04-12, FR-01-05) | AI assistant | 2026-11-23 |
| Lane names match the Context Diagram | Pass | AI assistant | 2026-11-23 |
| Renders (Mermaid 12.3.0, swimlane-beta, Chrome) | Pass | AI assistant | 2026-11-23 |
| AI critic prompt run, findings resolved or logged | Not yet run by the team | | |
