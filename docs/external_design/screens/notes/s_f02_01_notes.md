# Wireframe notes: S-F02-01 Book reviews

Actor: Reader · Frame: 360px · UI conventions: v0.8 · Author: Hoa

## Elements
| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Back and screen title | Screen header | Back to existing OPAC Book Detail; title “Đánh giá sách” | — |
| 2 | Book context | Book row | Book catalogue › title, author plus neutral grey “Cover” placeholder, no Format label (D21): “Principles of Economics” · N. Gregory Mankiw | FR-02-02 |
| 3 | Review editor | Text area with counter | Book review › review text; plain text, 1–2,000 characters; counter n/2.000; in edit mode pre-fills existing review text and shows cancel action | FR-02-01, FR-02-03, FR-02-11 |
| 4 | Anonymous posting | Checkbox | Reader accounts › full registered name; unchecked by default, checked displays “Bạn đọc ẩn danh” | FR-02-22 |
| 5 | Review hint | Text area with counter | Hint line under the review field, small muted text: “Đánh giá không được chứa từ ngữ xúc phạm, quảng cáo hoặc thông tin cá nhân.” (MSG-14, D20); not a link | D20 |
| 6 | Submit review | Primary button | “Đăng đánh giá” / “Lưu thay đổi” when editing | FR-02-01, FR-02-03 |
| 7 | Own review | Review item | Book review › review text, reviewer, posted date, is own review (no review ID code on UI); text buttons “Sửa”, “Xoá đánh giá” | FR-02-03, FR-02-04 |
| 8 | Other readers’ reviews | Review item | Book review › review text, reviewer, posted date (no review ID code on UI); text button “Báo cáo đánh giá” on S-F02-01 only | FR-02-02, FR-02-13, FR-02-09, FR-02-21 |
| 9 | Next page | Load more button | “Xem thêm đánh giá”; appends the next 10 reviews, newest first; shown while more published reviews remain (D6) | FR-02-02 |
| 10 | Empty list message | Empty state | “Không có đánh giá nào để hiển thị. Hãy là người đầu tiên viết đánh giá cho cuốn sách này.” (or book-not-found variant when book does not exist); replaces review list | FR-02-15 |
| 11 | Page-level feedback | Banner | MSG-04 network error; “Bạn đã báo cáo đánh giá này.” for duplicate report; “Bạn không thể báo cáo đánh giá của chính mình.” for the reader's own review (D39); “Không thể thực hiện thao tác trên đánh giá không thuộc về bạn.” for non-owner edit/delete | FR-04-20, FR-02-21, FR-02-24, FR-02-11 |
| 12 | Field validation feedback | Inline error | Empty review text / over 2,000 characters (inline error message under field) | FR-02-01, FR-02-11 |
| 13 | Success confirmation | Toast | “Đã đăng đánh giá.” / “Đã cập nhật đánh giá.” / “Đã xoá đánh giá.” / “Đã gửi báo cáo.” | FR-02-12, FR-02-09 |
| 14 | Loading placeholder | Skeleton | Same shape as book context, form and review list | MSG-05 |
| 15 | Retry action | Secondary button | “Thử lại” inside MSG-04 Banner | FR-04-20 |

## States drawn
| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | [s_f02_01.png](../img/s_f02_01/s_f02_01.png) | Book context, review editor, own review, other reviews (10 per page, no review IDs), text-button actions, and next-page action | FR-02-01, FR-02-02, FR-02-03, FR-02-04, FR-02-09 |
| Empty | [s_f02_01_empty.png](../img/s_f02_01/s_f02_01_empty.png) | Book exists but has no published reviews; empty state message with prompt to write the first review, no review list | FR-02-15 |
| Loading | [s_f02_01_loading.png](../img/s_f02_01/s_f02_01_loading.png) | Skeleton blocks replace content; no loading text | MSG-05 |
| Error | [s_f02_01_error.png](../img/s_f02_01/s_f02_01_error.png) | Page content preserved; empty or over-limit review text with Inline error; error-numbered image included | FR-02-01, FR-02-11 |
| Error-2 | [s_f02_01_error_2.png](../img/s_f02_01/s_f02_01_error_2.png) | Page content preserved; MSG-04 network error Banner with “Thử lại” button; numbered variant included | FR-04-20 |
| Error-3 | [s_f02_01_error_3.png](../img/s_f02_01/s_f02_01_error_3.png) | Page content preserved; Banner with “Bạn đã báo cáo đánh giá này.” or non-owner action message; numbered variant included. “Bạn không thể báo cáo đánh giá của chính mình.” uses the same Banner (D39) | FR-02-21, FR-02-24, FR-02-11 |
| Error-4 | [s_f02_01_error_4.png](../img/s_f02_01/s_f02_01_error_4.png) | Banner “Bạn không thể báo cáo đánh giá của chính mình.”; no report saved (D39) | FR-02-24 |
| Success | [s_f02_01_success.png](../img/s_f02_01/s_f02_01_success.png) | Confirmation toast (“Đã đăng đánh giá.” / “Đã gửi báo cáo.”) and refreshed review list preserving existing reviews (including own review and #91) | FR-02-12, FR-02-09 |

## Actions and where they go
| Element | User action | Goes to |
|---|---|---|
| Back | tap | Existing OPAC Book Detail (exit) |
| Review editor / Submit review | enter plain text and submit | stays |
| Review editor / Submit while signed out | request sign-in | M-F00-01 (reused; owned by Ha), then S-F00-01 → S-F00-02 → S-F02-01 |
| Own review / Sửa | edit own review text and save | stays; if signed out, M-F00-01 then return to S-F02-01 |
| Own review / Xoá đánh giá | request deletion | M-F02-01-01; if signed out, M-F00-01 then return to S-F02-01 |
| Other review / Báo cáo đánh giá | request report | M-F02-01-02 |
| Report while signed out | request sign-in | M-F00-01 (reused; owned by Ha), then S-F00-01 → S-F00-02 → S-F02-01 |
| Xem thêm đánh giá | request next page | stays |
| Thử lại | retry after load failure | stays |

## Open questions

None. Decisions: see [decision_index.md](../../../project_brief/decision_index.md#s-f02-01).