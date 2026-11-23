# Wireframe notes: S-F02-04 Reported reviews

Actor: On-site Staff · Frame: 1280px · UI conventions: v0.8 · Author: Hoa

## Elements
| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Back and screen title | Screen header | “Đánh giá bị báo cáo”; Back to S-F04-01 | — |
| 2 | Open report queue | Review item | Book review › report, review text, reviewer, posted date; Open reports #91 and #95 | FR-02-14, FR-02-19 |
| 3 | Selected review detail | Review item | Selected review (#91 initially, then #95 after handling #91), text and reviewer; staff judges content manually | FR-02-10, FR-02-20 |
| 4 | Remove selected review | Primary button | “Gỡ đánh giá” opens confirmation modal; confirmation itself uses Destructive button | FR-02-10 |
| 5 | Dismiss selected report | Secondary button | “Bỏ qua báo cáo”; review stays public and leaves queue | FR-02-20 |
| 6 | Empty queue message | Empty state | “Không có đánh giá bị báo cáo nào đang chờ xử lý.” | FR-02-19 |
| 7 | Page feedback | Banner | MSG-04 network error | FR-04-20, FR-02-10, FR-02-20 |
| 8 | Loading placeholder | Skeleton | Queue and selected review detail placeholders | MSG-05 |
| 9 | Success confirmation | Toast | “Đã gỡ đánh giá.” / “Đã bỏ qua báo cáo.” with refreshed queue | FR-02-10, FR-02-20 |
| 10 | Retry action | Secondary button | “Thử lại” inside MSG-04 Banner | FR-04-20 |
| 11 | Sign out | Secondary button | «Đăng xuất» at the right of the screen header, every state and behind M-F02-04-01; staff stay signed in until they sign out (D7) | FR-04-21 |

## States drawn
| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | [s_f02_04.png](../img/s_f02_04/s_f02_04.png) | Header with «Đăng xuất» at the right; open reports #91 and #95 in queue; #91 selected; Remove and Dismiss actions; numbered variant in [s_f02_04_numbered.png](../img/s_f02_04/s_f02_04_numbered.png) (#1–#5, #11; re-exported 22/11/2026) | FR-02-14, FR-02-10, FR-02-20 |
| Empty | [s_f02_04_empty.png](../img/s_f02_04/s_f02_04_empty.png) | Header with «Đăng xuất»; no reported reviews are waiting | FR-02-19 |
| Loading | [s_f02_04_loading.png](../img/s_f02_04/s_f02_04_loading.png) | Header with «Đăng xuất»; skeleton queue and detail | MSG-05 |
| Error | [s_f02_04_error.png](../img/s_f02_04/s_f02_04_error.png) | Single header with «Đăng xuất»; MSG-04 Banner with retry action; no Empty or Toast | FR-04-20 |
| Success | [s_f02_04_success.png](../img/s_f02_04/s_f02_04_success.png) | Header with «Đăng xuất»; remove outcome: #91 leaves queue and public display; #95 remains in queue/detail for next step (d5); toast “Đã gỡ đánh giá.” | FR-02-10, FR-04-12 |
| Success-2 | [s_f02_04_success_2.png](../img/s_f02_04/s_f02_04_success_2.png) | Header with «Đăng xuất»; dismiss outcome: #91 leaves queue but stays public; #95 remains in queue/detail for next step (d5); toast “Đã bỏ qua báo cáo.” | FR-02-20 |

## Actions and where they go
| Element | User action | Goes to |
|---|---|---|
| Back | tap | S-F04-01 |
| Đăng xuất | click | S-F00-03 (staff session ends; FR-04-21) |
| Queue item | select a reported review | stays (detail updates on S-F02-04) |
| Gỡ đánh giá | select Remove | M-F02-04-01 |
| Bỏ qua báo cáo | dismiss the report | stays (review remains public; report leaves queue) |
| Thử lại | retry after load failure | stays |
| Confirm Gỡ đánh giá | confirm removal | stays (review removed from public display; audit entry written) |
| Cancel modal | cancel removal | stays (review remains public and in queue) |

## Open questions
None. Decisions: see [decision_index.md](../../../project_brief/decision_index.md#s-f02-04).