# Không có âm thanh, micro không hoạt động trong cuộc họp

| | |
| --- | --- |
| Cấp độ | L1 |
| Mức ưu tiên thường gặp | P3; P2 nếu đang trong cuộc họp lãnh đạo hoặc hội thảo quan trọng |
| Thời gian xử lý ước tính | 10-20 phút |
| Cần quyền quản trị | Không, trừ khi cài driver |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Không nghe được âm thanh trong Teams/Zoom.
- Người khác không nghe thấy người dùng nói.
- Tai nghe hoạt động trong ứng dụng này nhưng không hoạt động trong ứng dụng khác.

## Câu hỏi cần hỏi người dùng trước

- Dùng loa/micro tích hợp, tai nghe USB, Bluetooth hay jack 3.5 mm?
- Lỗi xảy ra trong Teams, Zoom hay toàn bộ Windows?
- Thiết bị có nút mute vật lý không?

## Kiểm tra nhanh

- Kiểm tra nút gạt/bấm tắt tiếng (Mute vật lý) trên thân tai nghe hoặc trên dây cáp.
- Mở **Settings** > **Privacy & security** > **Microphone** và kiểm tra *"Microphone access"* cùng *"Let apps access your microphone"* có đang được BẬT (On) không.
- Kiểm tra cài đặt thiết bị (Device Settings) ngay trong cuộc họp Teams/Zoom xem đã chọn đúng tên tai nghe hay đang chọn nhầm thiết bị khác.

## Nguyên nhân thường gặp

1. Chọn sai thiết bị đầu vào/đầu ra.
2. Micro bị mute trong ứng dụng hoặc trên tai nghe.
3. Quyền microphone/camera bị tắt trong Windows.
4. Bluetooth headset đang ở profile chất lượng thấp.
5. Driver âm thanh lỗi.

## Các bước xử lý

### Bước 1: Kiểm tra mức âm lượng và mute

Kiểm tra volume Windows, nút mute trên tai nghe, nút mute trong Teams/Zoom và mixer âm lượng.

### Bước 2: Chọn đúng thiết bị trong Windows

Settings > System > Sound:

- Output: chọn loa/tai nghe đúng.
- Input: chọn micro đúng và thử **Test your microphone**.

### Bước 3: Chọn đúng thiết bị trong ứng dụng họp

Trong Teams/Zoom > Settings > Audio, chọn speaker và microphone đúng. Chạy test call nếu có.

### Bước 4: Kiểm tra quyền microphone

Settings > Privacy & security > Microphone, bật quyền truy cập microphone cho desktop apps.

### Bước 5: Cắm lại hoặc pair lại thiết bị

Với USB/Bluetooth, rút cắm lại hoặc remove/pair lại. Nếu dùng Bluetooth, thử tai nghe có dây để xác định lỗi do headset hay Windows.

## Khi nào chuyển cấp (escalate)

- Driver âm thanh lỗi sau cập nhật Windows.
- Micro tích hợp không hoạt động cả trong nhiều ứng dụng và nhiều tài khoản.
- Thiết bị họp phòng meeting cần cấu hình chuyên dụng.

**Thông tin đính kèm ticket:** thiết bị audio, app bị lỗi, ảnh cài đặt Sound, kết quả test call.

## Phòng ngừa

- Chuẩn hóa tai nghe USB cho nhân viên họp nhiều.
- Hướng dẫn kiểm tra audio trước cuộc họp quan trọng.
- Cập nhật driver âm thanh qua công cụ quản lý thiết bị.

## Mẫu ghi chú đóng ticket

> Nguyên nhân: Teams đang chọn micro của màn hình thay vì tai nghe USB. Cách xử lý: chọn lại thiết bị audio trong Teams, test call nghe nói bình thường.

