# Information Architecture – Lời mời sinh nhật 28/10

Trang đơn (single page), đi tuần tự từng màn hình, không có menu.

```
index.html
│
├── 1. Phong bì (s-envelope)
│     └── Phong bì 💌 + gợi ý "chạm để mở"          → [chạm] → 2
│
├── 2. Lá thư (s-letter)
│     ├── Lời chào "Gửi <tên em>"
│     ├── Thư hiện từng chữ (chạm để hiện hết)
│     └── Nút "Đọc tiếp nè"                          → 3
│
├── 3. Kế hoạch (s-plan)
│     ├── Ngày: Thứ, 28/10/YYYY
│     ├── Đếm ngược: Ngày / Giờ / Phút / Giây
│     ├── Lịch trình (giờ · hoạt động · mô tả)
│     └── Nút "Vậy em có đồng ý không?"              → 4
│
├── 4. Câu hỏi (s-ask)
│     ├── "Em đi chơi với anh vào sinh nhật nhé?"
│     ├── Nút "Đồng ý" (to dần lên)                  → 5
│     └── Nút "Không" (chạy trốn, đổi chữ)
│
├── 5. Chọn món ăn (s-food)                ← MỚI
│     ├── Món chính      (bắt buộc, chọn 1)
│     ├── Tráng miệng    (tùy chọn, chọn 1)
│     ├── Đồ uống        (tùy chọn, chọn 1)
│     ├── Ghi chú cho anh (ô nhập, tùy chọn)
│     └── Nút "Chốt món" (khóa khi chưa chọn món chính) → 6
│
└── 6. Kết (s-yes)
      ├── Tim đập + pháo giấy
      ├── Lời nhắn cuối
      ├── Tóm tắt lựa chọn của em (món chính, tráng miệng, đồ uống, ghi chú)
      ├── Nút "Gửi cho anh" (chia sẻ qua Messenger/Zalo…, hoặc sao chép)
      ├── Nút "Chọn lại món"                          → 5
      └── Chữ ký "— Anh —"
```

## Dữ liệu cấu hình (`CONFIG` trong `<script>`)

| Khóa         | Ý nghĩa                                                 |
|--------------|---------------------------------------------------------|
| `herName`    | Tên / biệt danh của cô ấy                               |
| `yourName`   | Tên người gửi                                           |
| `birthday`   | Ngày + tháng sinh nhật                                  |
| `meetTime`   | Giờ đón (mốc đếm ngược)                                 |
| `letter`     | Nội dung lá thư                                         |
| `plan[]`     | Lịch trình: `icon`, `time`, `title`, `desc`             |
| `notifyEmail`| Email nhận lựa chọn món (`''` để tắt)                   |
| `food`       | Các nhóm món: `main`, `dessert`, `drink` → `[{icon, name}]` |
| `finalMsg`   | Lời nhắn ở màn hình cuối                                |

## Lưu & gửi lựa chọn

- Lựa chọn được lưu trong trình duyệt của cô ấy (localStorage).
- Khi bấm **Chốt món**, lựa chọn được **tự động gửi về email** `CONFIG.notifyEmail` qua FormSubmit
  (dịch vụ miễn phí, không cần server). Chốt lại y nguyên thì không gửi trùng; gửi lỗi thì lần chốt sau gửi lại.
- Lần gửi đầu tiên, FormSubmit gửi email **kích hoạt** đến hộp thư – phải bấm xác nhận một lần thì các lần sau mới tới.
- Nút **Gửi cho anh** vẫn giữ làm phương án dự phòng (Web Share API / sao chép).

## Giao diện

- `index.html` – **Game pixel** (đang dùng). Đổi tên màn hình theo kiểu game:
  1 Start (`PRESS START`) · 2 Hộp thoại RPG · 3 `QUEST LOG` · 4 `NEW QUEST!` · 5 `ITEM SHOP` · 6 `QUEST ACCEPTED!`.
  Thanh HP (tim) ở trên cùng = tiến trình, có âm thanh 8-bit (bật/tắt bằng nút `SFX`).
  Chữ có dấu dùng font VT323; font Press Start 2P chỉ dùng cho nhãn tiếng Anh không dấu.
- `index-dem-sao.html` – bản thay thế **Đêm đầy sao** (cùng nội dung, cùng luồng).
