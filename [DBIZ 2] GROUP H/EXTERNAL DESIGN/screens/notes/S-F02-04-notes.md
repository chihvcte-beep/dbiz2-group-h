# Wireframe notes: S-F02-04 Reported reviews

Actor: On-site Staff · Frame: 1280px · UI conventions: v0.7 · Author: Hoa

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

## States drawn
| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | img/S-F02-04.png | Open reports #91 and #95 in queue; #91 selected; Remove and Dismiss actions; numbered variant in S-F02-04-numbered.png | FR-02-14, FR-02-10, FR-02-20 |
| Empty | img/S-F02-04-empty.png | No reported reviews are waiting | FR-02-19 |
| Loading | img/S-F02-04-loading.png | Skeleton queue and detail | MSG-05 |
| Error | img/S-F02-04-error.png | Single header; MSG-04 Banner with retry action; no Empty or Toast | FR-04-20 |
| Success | img/S-F02-04-success.png | Remove outcome: #91 leaves queue and public display; #95 remains in queue/detail for next step (d5); toast “Đã gỡ đánh giá.” | FR-02-10, FR-04-12 |
| Success-2 | img/S-F02-04-success-2.png | Dismiss outcome: #91 leaves queue but stays public; #95 remains in queue/detail for next step (d5); toast “Đã bỏ qua báo cáo.” | FR-02-20 |

## Actions and where they go
| Element | User action | Goes to |
|---|---|---|
| Back | tap | S-F04-01 |
| Queue item | select a reported review | stays (detail updates on S-F02-04) |
| Gỡ đánh giá | select Remove | M-F02-04-01 |
| Bỏ qua báo cáo | dismiss the report | stays (review remains public; report leaves queue) |
| Thử lại | retry after load failure | stays |
| Confirm Gỡ đánh giá | confirm removal | stays (review removed from public display; audit entry written) |
| Cancel modal | cancel removal | stays (review remains public and in queue) |

## Open questions
| # | Question | Default drawn |
|---|---|---|
| 1 | [NEEDS CLARIFICATION: The source docs specify selecting a report and reading its review, but do not prescribe the queue/detail layout. Is a two-column queue plus detail view acceptable?] | Use two columns at 1280px as a provisional layout; only show source-backed data and actions. |
| 2 | [NEEDS CLARIFICATION: Does success wording need a separate message for Dismiss versus Remove?] | Use action-specific toast copy; no new status/dashboard. |
| 3 | [NEEDS CLARIFICATION: Is there a staff-approved display field for report reason?] | No report-reason field is shown because no reason data is specified by the AD/FR excerpts. |