# Wireframe notes: M-F02-03-01 QR label sheet preview

Actor: On-site Staff · Frame: 1280px · UI conventions: v0.8 · Author: Ha

## Elements

| # | Element | Component | Content / data source | FR |
| --- | --- | --- | --- | --- |
| 1 | Title | Modal | Xem trước trang nhãn mã QR | FR-02-08 |
| 2 | A4 preview | Label sheet | Book QR codes › QR code; Book catalogue › title; Book placement & library layout › floor, room code, shelf code of the book's primary shelf location returned by the sync (same as S-F01-01; D13) | FR-02-08 |
| 3 | Print | Primary button | In | FR-02-08 |
| 4 | Close | Secondary button | Đóng — records nothing; the books stay in the S-F02-03 list with their ticks kept (D12, D18) | FR-02-08 |
| 5 | Omitted books | Banner | Book catalogue › title for each book left out (partial success only) | FR-02-18 |
| 6 | Printed | Secondary button | Đã in xong, next to In / Đóng — records each book on the sheet as label-printed; on a reprint it writes only the audit entry; «In» stays the only Primary button (D12, D17, D40) | FR-02-08, FR-02-25 |
| 7 | Sheet pages | Selection counter | Trang A4 <n> / <m> · <k> nhãn, only when the sheet has more than one A4 page (D41) | FR-02-08 |

## States drawn

| State | Image | What the user sees | FR |
| --- | --- | --- | --- |
| Default | [m_f02_03_01.png](../img/m_f02_03_01/m_f02_03_01.png), [m_f02_03_01_numbered.png](../img/m_f02_03_01/m_f02_03_01_numbered.png) | A4 3 × 8 preview with three labels and In / Đã in xong / Đóng. | FR-02-08 |
| Empty | Not applicable: validation keeps the user on S-F02-03. | — | — |
| Loading | Not applicable: the preview opens after the sheet is ready. | — | — |
| Error | Not applicable: validation and failures are shown on S-F02-03. | — | — |
| Success — partial | [s_f02_03_success.png](../img/s_f02_03/s_f02_03_success.png) | Two-label A4 preview and the omitted book name. | FR-02-08, FR-02-18 |
| More than one A4 page | [m_f02_03_01_multipage.png](../img/m_f02_03_01/m_f02_03_01_multipage.png) | First A4 page of a 25-label sheet; #7 shows the page count (D41). | FR-02-08 |
| Reprint | [m_f02_03_01_reprint.png](../img/m_f02_03_01/m_f02_03_01_reprint.png) | Same QR code and title, no shelf location (D40). | FR-02-25 |

## Actions and where they go

| Element | User action | Goes to |
| --- | --- | --- |
| Print | Open the browser print dialog (AD-UC-10 a5). | Browser print dialog (exit) |
| Close | Dismiss the preview without confirming, e.g. after a failed print (AD-UC-10 a9). Nothing is recorded; the books stay listed with their ticks kept, so staff can print again (D12, D18). | S-F02-03 |
| Printed | Choose «Đã in xong» after the labels are printed (AD-UC-10 a8). Each book on the sheet is recorded as label-printed and leaves the list (FR-02-08; D12). On a reprint only the audit entry is written and the books stay in the Đã in nhãn list (FR-02-25; D40). | S-F02-03 |

## Open questions

None. Decisions: see [decision_index.md](../../../project/decision_index.md#m-f02-03-01).
