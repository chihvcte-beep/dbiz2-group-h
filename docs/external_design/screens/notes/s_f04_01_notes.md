# Wireframe notes: S-F04-01 Staff page

Actor: On-site Staff · Frame: 1280px · UI conventions: v0.8 · Author: Ha

## Elements

| # | Element | Component | Content / data source | FR |
| --- | --- | --- | --- | --- |
| 1 | Title | Screen header | Trang nhân viên | FR-04-07 |
| 2 | Print QR labels | Menu tile | In nhãn mã QR | FR-02-08 |
| 3 | Reported reviews | Menu tile | Đánh giá bị báo cáo (Could) | FR-02-14 |
| 4 | Staff page loading | Skeleton | MSG-05 | FR-04-08 |
| 5 | Network error | Banner | MSG-04 | FR-04-20 |
| 6 | Try again | Secondary button | Thử lại | FR-04-20 |
| 7 | Sign out | Secondary button | Đăng xuất, in the Screen header → S-F00-03 (D7) | FR-04-21 |

## States drawn

| State | Image | What the user sees | FR |
| --- | --- | --- | --- |
| Default | [s_f04_01.png](../img/s_f04_01/s_f04_01.png), [s_f04_01_numbered.png](../img/s_f04_01/s_f04_01_numbered.png) | Two staff task tiles. | FR-04-07 |
| Empty | Not applicable: the menu has fixed options. | — | — |
| Loading | [s_f04_01_loading.png](../img/s_f04_01/s_f04_01_loading.png), [s_f04_01_loading_numbered.png](../img/s_f04_01/s_f04_01_loading_numbered.png) | Skeleton while opening the staff page. | FR-04-08 |
| Error | [s_f04_01_error.png](../img/s_f04_01/s_f04_01_error.png), [s_f04_01_error_numbered.png](../img/s_f04_01/s_f04_01_error_numbered.png) | MSG-04. Requests without a staff session open S-F00-03. | FR-04-20, FR-04-08 |
| Success | Not applicable: opening the menu uses its default state. | — | — |

## Actions and where they go

| Element | User action | Goes to |
| --- | --- | --- |
| Staff page address | Open with valid staff session, or route to staff sign-in. | S-F04-01 / S-F00-03 |
| Print QR labels | Open QR label printing. | S-F02-03 |
| Reported reviews | Open the reported reviews list if UC-13 ships. | S-F02-04 |
| Try again | Retry after a network failure. | stays |
| Sign out | End the staff session (FR-04-21). | S-F00-03 |

## Open questions

None. Decisions: see [decision_index.md](../../../project/decision_index.md#s-f04-01).
