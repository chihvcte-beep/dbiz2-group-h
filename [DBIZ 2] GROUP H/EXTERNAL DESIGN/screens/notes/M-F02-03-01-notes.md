# Wireframe notes: M-F02-03-01 QR label sheet preview

Actor: On-site Staff · Frame: 1280px · UI conventions: v0.7 · Author: Ha

## Elements

| # | Element | Component | Content / data source | FR |
| --- | --- | --- | --- | --- |
| 1 | Title | Modal | Xem trước trang nhãn mã QR | FR-02-08 |
| 2 | A4 preview | Label sheet | Book QR codes › QR code; Book catalogue › title; Book placement & library layout › floor, room code, shelf code | FR-02-08 |
| 3 | Print | Primary button | In | FR-02-08 |
| 4 | Close | Secondary button | Đóng | FR-02-08 |
| 5 | Omitted books | Banner | Book catalogue › title for each book left out (partial success only) | FR-02-18 |

## States drawn

| State | Image | What the user sees | FR |
| --- | --- | --- | --- |
| Default | img/M-F02-03-01.png, img/M-F02-03-01-numbered.png | Preview with three labels and Print / Close. | FR-02-08 |
| Empty | Not applicable: validation keeps the user on S-F02-03. | — | — |
| Loading | Not applicable: the preview opens after the sheet is ready. | — | — |
| Error | Not applicable: validation and failures are shown on S-F02-03. | — | — |
| Success — partial | img/S-F02-03-success.png | Two-label A4 preview and the omitted book name. | FR-02-08, FR-02-18 |

## Actions and where they go

| Element | User action | Goes to |
| --- | --- | --- |
| Print | Open the browser print dialog (AD-UC-10 a5). | stays |
| Close | Dismiss the preview and return to book selection (AD-UC-10 a4). | S-F02-03 |

## Open questions

Review status: self-checked against the assignment and the two shared UI/UX handbooks. Cross-review by Hoa and final consistency review by Linh are pending.

| # | Question | Default drawn |
| --- | --- | --- |
| 1 | [NEEDS CLARIFICATION: Which fields besides QR should go on the label?] | QR placeholder, book title and shelf location as suggested in v0.7 §3. |
| 2 | [NEEDS CLARIFICATION: How many labels per A4 page?] | A4 portrait, provisional 2 columns × 5 rows (10 per sheet). The sample only fills two or three cells. |
