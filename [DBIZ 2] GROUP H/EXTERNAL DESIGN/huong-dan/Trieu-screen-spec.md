# Screen Spec — phần việc của Trieu

| Mục | Nội dung |
|---|---|
| Người thực hiện | **Trieu** |
| Đọc kèm | `huong-dan/screen-spec-chung.md` (luật chung, cách điền, lời nhắc AI, checklist) |
| Phiên bản | v1.0 · 19/11/2026 |
| Soát chéo | Bạn soát spec của **Nhi**; **Nhi** soát spec của bạn |

## 1. Spec bạn viết

| # | Tệp | Màn hình | Actor · khổ | Priority | AD |
|---|---|---|---|---|---|
| 1 | `screen-spec-S-F03-02.md` | Reading history and preferences | Reader · 360px | Should | AD-UC-07 |
| 2 | `screen-spec-S-F03-06.md` | AI chatbot book search | Reader · 360px | Could | AD-UC-08 |
| 3 | `screen-spec-S-F03-07.md` | Book recommendations | Reader · 360px | Could | AD-UC-09 |

Không có modal riêng. Cả 3 màn mở **M-F00-01** khi chưa đăng nhập → trỏ về
`screen-spec-S-F00-01.md §3.1`, ghi rõ **biến thể câu chữ** nào được dùng (chatbot FR-03-18, gợi ý sách
FR-03-21).

FR của từng màn: cột "UC / FR" trong `screen-list.md`, cộng **FR-04-20** nếu có trạng thái lỗi mạng.

## 2. Việc phải làm trước (hạn 21/11)

1. **Xuất ảnh riêng** từ `screens/src/S-F03-0x.html` theo tên ở phần "States drawn" của tệp ghi chú.
2. **Ảnh đánh số đang sai khổ:** 1740px — cần **1080px** (khung 360px × DPR 3, bước 5 của hướng dẫn
   wireframe).
3. Ba tệp HTML của bạn đang tự chứa màu và kiểu riêng, chưa dùng `tokens.css`. Linh sẽ soát ở bảng
   Consistency review; nếu Linh yêu cầu chuyển sang `tokens.css` thì sửa HTML rồi xuất lại ảnh trước
   khi viết spec.
4. Xoá tệp `trieu-wireframe-4-upload.zip` ở thư mục gốc kho (bản trùng của các tệp đã có) — hoặc
   nhờ trưởng nhóm xoá.

## 3. Lưu ý riêng từng spec

### S-F03-02
- Ô tiến độ: số nguyên 0–100 (FR-03-04); nhập 120% khi đang 20% → lỗi, giữ dữ liệu cũ (FR-03-22,
  AD-UC-07 mục 3). Ghi đủ ở cột Validation và dòng Error.
- Được đánh dấu "Đã đọc xong" khi tiến độ dưới 100% (AD-UC-07 câu hỏi 4) — quy tắc ở mục 6.
- Phần sở thích đọc là phần Could (FR-03-05); chủ đề chỉ chọn trong danh sách chủ đề của danh mục.
- Back về nơi đã mở (khu vực cá nhân OPAC, hoặc S-F03-07).

### S-F03-06
- Chỉ hỏi đăng nhập **sau khi gửi tin đầu tiên**, không phải khi mở màn (L8-05) — quy tắc ở mục 6.
- Lỗi AI → liên kết "dùng bộ lọc định dạng" → S-F03-01 (FR-03-17); không có kết quả → câu trả lời
  gợi ý thử từ khác (FR-03-16). Đây là trạng thái, không phải màn mới.
- Thẻ sách → `Existing OPAC Book Detail (exit)`.
- Các câu đã chốt ngày 04/11 (thời gian chờ 10 giây, không xoá hội thoại…): ghi Status
  `Closed 04/11/2026: …` ở mục 9.

### S-F03-07
- Danh sách 10 sách (AD-UC-09 câu hỏi 3); bổ sung sách xu hướng khi danh sách ngắn (FR-03-20);
  chưa có dữ liệu → sách phổ biến kèm lời mời đặt sở thích → S-F03-02 (FR-03-19).
- Nhãn "Xu hướng" là phương án bạn tự thêm — giữ ở mục 9 cho đến khi nhóm chốt.
