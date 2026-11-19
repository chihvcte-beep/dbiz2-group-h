# Screen Spec — phần việc của Nhi

| Mục | Nội dung |
|---|---|
| Người thực hiện | **Nhi** |
| Đọc kèm | `huong-dan/screen-spec-chung.md` (luật chung, cách điền, lời nhắc AI, checklist) |
| Phiên bản | v1.0 · 19/11/2026 |
| Soát chéo | Bạn soát spec của **Trieu** và spec S-F03-01 Linh viết từ wireframe của bạn; **Trieu** soát spec của bạn |

## 1. Spec bạn viết

| # | Tệp | Màn hình | Actor · khổ | Priority | AD |
|---|---|---|---|---|---|
| 1 | `screen-spec-S-F01-01.md` | Shelf location (with Save to my list) | Reader · 360px | Must | AD-UC-01, AD-UC-12 |
| 2 | `screen-spec-S-F01-02.md` | Interactive digital library map | Reader · 360px | Must | AD-UC-01, AD-UC-02 |
| 3 | `screen-spec-S-F03-03.md` | Saved books list | Reader · 360px | Should | AD-UC-12 |

Bạn không có modal riêng. S-F01-01 (Save) và S-F03-03 mở **M-F00-01** khi chưa đăng nhập → ở mục 5
ghi `Goes to: M-F00-01 (see screen-spec-S-F00-01.md §3.1)`, không chép nội dung modal.

FR của từng màn: cột "UC / FR" trong `screen-list.md`, cộng **FR-04-20** nếu wireframe có trạng thái
lỗi mạng.

## 2. Việc phải làm trước (hạn 21/11)

1. **Xuất ảnh riêng cho cả 4 wireframe bạn đã vẽ**, kể cả S-F03-01 (Linh viết spec), theo tên ở phần
   "States drawn" của tệp ghi chú.
2. **Ảnh đánh số đang sai khổ:** S-F01-01, S-F03-01, S-F03-03 rộng 1740px — cần **1080px** (khung
   360px × DPR 3). S-F01-02 đã đúng.
3. Đưa mã nguồn wireframe vào `screens/src/` (hiện chưa có).
4. S-F01-02: tệp ghi chú ghi ảnh đánh số thiếu số 2 (tiêu đề). Quyết định một lần: hoặc thêm số 2
   vào ảnh, hoặc đánh lại số trong tệp ghi chú cho khớp — mục 3 của spec phải khớp ảnh.
5. Tệp ghi chú S-F01-02 chưa ghi `Author` ở dòng đầu — bổ sung.

## 3. Lưu ý riêng từng spec

### S-F01-01
- Mỗi bản sách một dòng "Tầng · Phòng · Kệ" (định dạng ở ui-conventions §2).
- Mục 4 có nhiều trạng thái: chỉ có bản online (FR-01-06), không có vị trí kệ (FR-01-07), đã lưu
  (FR-03-06), đã lưu từ trước (FR-03-24). Câu chữ lấy từ ui-conventions §4.
- Mục 6: nút Lưu chỉ hiện với sách giấy (L8-06); không có liên kết sang danh sách đã lưu.
- "View on map" là phần Could (FR-01-03) — ghi rõ ở mục 6 để có thể cắt mà không bỏ màn hình.

### S-F01-02
- Hai điểm vào khác nhau (menu OPAC → tầng thấp nhất; "View on map" → phòng của sách được tô sáng).
  Mục 1 và mục 4 phải tách rõ hai trường hợp; Back đi về hai nơi khác nhau.
- Lỗi "Map unavailable" và "Room cannot be identified" hiện **trên S-F01-02**, thông tin kệ vẫn hiện
  (L8-11).
- Phòng phân biệt bằng viền/ký hiệu, không chỉ bằng màu (mục 8).

### S-F03-03
- Một sách không có vị trí kệ là **trạng thái của dòng đó**, không phải trạng thái của cả màn
  (FR-01-07). Ghi ở mục 4 và mục 6.
- Remove là phần Could (FR-03-08).

## 4. Khi soát spec của Linh (S-F03-01)

Kiểm tra spec có **đúng với wireframe bạn vẽ** không: số `#`, câu chữ tiếng Việt, trạng thái chọn sẵn
khi mới mở, đích điều hướng. Ghi nhận xét trên pull request, không sửa hộ.
