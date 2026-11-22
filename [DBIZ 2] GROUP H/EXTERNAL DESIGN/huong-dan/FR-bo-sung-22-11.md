# Bổ sung FR theo quyết định nhóm ngày 22/11/2026

| Mục | Nội dung |
|---|---|
| Cập nhật | 22/11/2026 |
| Dành cho | Người giữ tệp `GROUP-H_UC_FR_COST.xlsx` |
| Nguồn | Group decision 22/11/2026 (Chi) — câu 3 (danh sách sách chờ in nhãn) và câu 7 (đăng xuất cho nhân viên); bổ sung cùng ngày: câu 12 (chỉ ghi nhận đã in nhãn khi nhân viên bấm «Đã in xong») và câu 13 (dùng vị trí kệ chính) |
| Đọc kèm | `ui-conventions.md` v0.9 mục 7 · `screen-list.md` · `ACTIVITY DIAGRAM/AD-UC-10.md` v1.4, `AD-UC-13.md` v1.4 |

Tệp này chỉ ghi **những dòng cần dán vào tệp Excel**. Tệp Excel chưa được sửa. Các tài liệu chung đã ghi
hai FR mới với chữ "proposed 22/11/2026"; khi bạn dán xong, báo lại để nhóm đổi thành "đã có trong W1".

## 1. Kiểm tra mã trước khi dán

Theo bản trích tệp Excel mới nhất nhóm có, mã cuối cùng của F-02 là **FR-02-22**, của F-04 là **FR-04-20**.
Vì vậy hai mã mới là **FR-02-23** và **FR-04-21**.

Trước khi dán, mở sheet W1_FunctionList và tìm hai mã này. Nếu đã có ai dùng, lấy số trống kế tiếp và báo
lại cho Chi để sửa các tài liệu chung.

## 2. Hai FR mới — dán vào W1_FunctionList

Dán **4 dòng** ngay dưới hai dòng FR-04-20, trước dòng "Totals". Thứ tự cột giống hệt các dòng đang có:

Feature · L2 ID · L2 function name · Actor · EARS acceptance criterion · Source trace · Dependency · Initial priority · FP type · L3 ID · Layer · L3 work item · Size · Base hours · EARS precise? · Hidden work? · New L2 · L2 index · FP value

| Feature | L2 ID | L2 function name | Actor | EARS acceptance criterion | Source trace | Dependency | Initial priority | FP type | L3 ID | Layer | L3 work item | Size | Base hours | EARS precise? | Hidden work? | New L2 | L2 index | FP value |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| F-02 | FR-02-23 | List physical books awaiting a QR label | Library Core System | WHEN signed-in On-site Staff open QR label printing, the system SHALL list the physical books in the synced catalogue that have not yet had a QR label printed, 20 per page, ordered by floor, room and shelf code of each book's primary shelf location returned by the sync. | UC:UC-10; Group decision 22/11/2026 (Chi) | FR-02-07 | Must | EQ | FR-02-23-FE | FE | Screen: list of physical books awaiting a QR label, 20 per page, ticks kept across pages, selected-books count | M | 8 | Yes | No | 1 | 78 | 4 |
| F-02 | FR-02-23 | List physical books awaiting a QR label | Library Core System | WHEN signed-in On-site Staff open QR label printing, the system SHALL list the physical books in the synced catalogue that have not yet had a QR label printed, 20 per page, ordered by floor, room and shelf code of each book's primary shelf location returned by the sync. | UC:UC-10; Group decision 22/11/2026 (Chi) | FR-02-07 | Must | EQ | FR-02-23-BE | BE | API: list physical books with no label printed yet, ordered by floor, room and shelf code of the primary shelf location from the sync, 20 per page | S | 4 | Yes | No | 0 | 78 | 0 |
| F-04 | FR-04-21 | Sign out of the staff page | Library Core System | WHEN signed-in On-site Staff choose Sign out, the system SHALL end the staff session and SHALL open the staff sign-in screen. The system SHALL keep the staff session valid until the staff member signs out (no time-out). | UC:UC-10; UC:UC-13; Group decision 22/11/2026 (Chi) | FR-04-07 | Should | NC | FR-04-21-FE | FE | Button "Đăng xuất" in the header of the staff page, QR label printing and reported reviews; open the staff sign-in after sign-out | S | 4 | Yes | No | 1 | 79 | 0 |
| F-04 | FR-04-21 | Sign out of the staff page | Library Core System | WHEN signed-in On-site Staff choose Sign out, the system SHALL end the staff session and SHALL open the staff sign-in screen. The system SHALL keep the staff session valid until the staff member signs out (no time-out). | UC:UC-10; UC:UC-13; Group decision 22/11/2026 (Chi) | FR-04-07 | Should | NC | FR-04-21-BE | BE | API: end the staff session; staff session stays valid with no time-out | S | 4 | Yes | No | 0 | 79 | 0 |

Ghi chú khi dán:

- **Ba cột cuối** (New L2, L2 index, FP value): nếu ở dòng trên các ô này là công thức, hãy **chép công thức của
  dòng trên** xuống thay vì gõ số. Số trong bảng là kết quả mong đợi: dòng đầu của mỗi FR có New L2 = 1; FR-02-23 là
  FR thứ 78, FR-04-21 là FR thứ 79; FP value lấy theo sheet Parameters (EQ = 4, NC = 0) và chỉ tính ở dòng đầu.
- Sau khi dán, dòng "Totals" phải thành **79 FR (L2) / 132 việc (L3)** (đang là 77 / 128).
- **Cỡ việc (Size, Base hours)** là đề xuất ban đầu của nhóm tài liệu; người tính chi phí xem lại.
- Cột **Dependency** ở dòng BE: các dòng cũ ghi không thống nhất (có dòng ghi chính mã của nó). Ở đây ghi FR mà
  chức năng này cần có trước, giống dòng FE.
- Lý do chọn loại FP: FR-02-23 chỉ **xem** danh sách, không thay đổi dữ liệu → EQ. FR-04-21 là quy tắc về phiên
  làm việc, không tạo hay sửa dữ liệu nghiệp vụ → NC.

## 3. FR-02-08 đổi câu chấp nhận (EARS)

Sửa ở **cả hai dòng** FR-02-08 (FR-02-08-FE và FR-02-08-BE), cột EARS acceptance criterion.

| | Câu chấp nhận |
|---|---|
| Cũ | WHEN signed-in On-site Staff select physical books and choose Print labels, the system SHALL produce a printable sheet of QR code labels for the selected books. |
| Mới | WHEN signed-in On-site Staff select physical books and choose Print labels, the system SHALL produce a printable sheet of QR code labels for the selected books, and WHEN the staff confirm that the sheet was printed («Đã in xong»), the system SHALL record that a label has been printed for each book on the sheet. |

Câu mới theo quyết định bổ sung (Group decision 22/11/2026 (Chi), câu 12): việc ghi nhận "đã in nhãn" **chỉ xảy ra khi
nhân viên bấm «Đã in xong»** trong khung xem trước trang nhãn, không phải lúc tạo trang nhãn. Nếu nhân viên bấm «Đóng»
hoặc in bị lỗi thì không ghi nhận gì, sách vẫn nằm trong danh sách chờ in nhãn. Câu ở bản trước ("…and SHALL record that
a label has been printed for each book included in the sheet.") không dùng nữa.

FR-02-23 (mục 2) cũng đã sửa theo câu 13: thứ tự tầng → phòng → kệ lấy theo **vị trí kệ chính** của sách do lần đồng bộ
trả về — cùng vị trí đang hiện ở màn vị trí kệ sách (S-F01-01) — kể cả khi một đầu sách có bản nằm ở nhiều kệ.

Hai điểm cần người giữ tệp xem thêm (nhóm tài liệu không tự quyết):

- FR-02-08 nay **có ghi lại dữ liệu** (sách nào đã in nhãn), nên loại FP có thể không còn là EQ (chỉ xem) mà là EI
  (có ghi dữ liệu). Xem lại cột FP type của FR-02-08.
- Việc ghi nhận "đã in nhãn" là phần việc mới thật sự. Theo luật của W4 ("chỉ đổi công sức khi phạm vi kỹ thuật
  thật sự đổi"), nhóm xem có cần nâng cỡ dòng FR-02-08-BE hoặc thêm một dòng việc mới không.

## 4. Mức ưu tiên đề xuất — dán vào W4_Prioritization

Dán 2 dòng ngay dưới dòng FR-04-20, trước "Control panel". Thứ tự cột: Feature · L2 ID · L2 function name ·
Initial priority · Rule applied · Kano category · New priority · Effective priority · Justification · Person-hours ·
Cost (VND). Hai cột cuối là công thức: chép công thức của dòng trên.

| Feature | L2 ID | L2 function name | Initial priority | Rule applied | Kano category | New priority | Effective priority | Justification (required if changed) | Person-hours | Cost (VND) |
|---|---|---|---|---|---|---|---|---|---|---|
| F-02 | FR-02-23 | List physical books awaiting a QR label | Must |  |  |  | Must |  | (công thức) | (công thức) |
| F-04 | FR-04-21 | Sign out of the staff page | Should |  |  |  | Should |  | (công thức) | (công thức) |

Vì sao đề xuất như vậy (để nhóm xác nhận):

- **FR-02-23 — Must** (luật R1): không có danh sách này, nhân viên không có chỗ để chọn sách cần in nhãn, nên FR-02-08
  (Must) không dùng được. Quyết định 22/11 không ghi mức ưu tiên cho FR này; đây là đề xuất của nhóm tài liệu.
  Sau khi dán, xem lại chỉ số "Must share" trong Control panel vẫn dưới 60%.
- **FR-04-21 — Should** (luật R2): theo quyết định 22/11/2026. Thiếu nút đăng xuất thì vẫn làm việc được, nhưng
  máy dùng chung ở thư viện sẽ để phiên nhân viên mở mãi.

## 5. Nhắc việc ở W2 (tính chi phí)

Các FR sau **có trong W1 và W4 nhưng chưa được tính chi phí ở W2** (đã kiểm ngày 22/11/2026 với ba FR đầu; hai FR
mới thì chưa có ở đâu cả):

| FR | Tên | Tình trạng |
|---|---|---|
| FR-02-22 | Post a review under the reader's name or anonymously | Có ở W1, W4; chưa tính ở W2 |
| FR-04-19 | Show the remaining OTP attempts | Có ở W1, W4; chưa tính ở W2 |
| FR-04-20 | Handle a network or loading error | Có ở W1, W4; chưa tính ở W2 |
| FR-02-23 | List physical books awaiting a QR label | Mới: dán W1, W4 (mục 2, 4) rồi tính ở W2 |
| FR-04-21 | Sign out of the staff page | Mới: dán W1, W4 (mục 2, 4) rồi tính ở W2 |

Thêm: nếu nhóm đổi cỡ việc của FR-02-08 (mục 3), tính lại FR-02-08 ở W2.

## 6. Sau khi dán xong

Báo cho Chi để:

- đổi chữ "proposed 22/11/2026" thành "có trong W1" ở `ui-conventions.md` (mục 7), `screen-list.md` (phần ghi chú
  dưới bảng) và `AD-UC-10.md`, `AD-UC-13.md` (phần Inputs);
- cập nhật mục "Open questions" số 1 của `ui-conventions.md`.
