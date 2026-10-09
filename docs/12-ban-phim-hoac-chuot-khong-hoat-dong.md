# Bàn phím hoặc chuột không hoạt động

| | |
| --- | --- |
| Cấp độ | L1 |
| Mức ưu tiên thường gặp | P3 |
| Thời gian xử lý ước tính | 5-20 phút |
| Cần quyền quản trị | Không, trừ khi cài driver |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Chuột không di chuyển, bàn phím không gõ được.
- Thiết bị Bluetooth mất kết nối.
- Một số phím hoặc nút không hoạt động.

## Câu hỏi cần hỏi người dùng trước

- Thiết bị có dây, USB receiver hay Bluetooth?
- Có bị sau khi đổi cổng USB, thay pin hoặc cập nhật Windows không?
- Thiết bị có hoạt động trên máy khác không?

## Kiểm tra nhanh

- Thử cắm đầu thu USB / cáp trực tiếp vào cổng USB trên thân máy (bỏ qua USB Hub hoặc Dock chuyển đổi).
- Bấm phím `Caps Lock` hoặc `Num Lock` trên bàn phím xem đèn LED trạng thái có sáng/tắt không (để biết máy có còn nhận tín hiệu từ bàn phím không).
- Với thiết bị không dây: Kiểm tra công tắc nguồn dưới đáy chuột/bàn phím và thay thử pin mới.

## Nguyên nhân thường gặp

1. Hết pin hoặc công tắc thiết bị đang tắt.
2. USB receiver lỏng hoặc cắm sai cổng.
3. Bluetooth bị tắt hoặc pairing lỗi.
4. Cổng USB, hub hoặc dock lỗi.
5. Driver HID lỗi.

## Các bước xử lý

### Bước 1: Kiểm tra phần cứng cơ bản

Thay pin, bật công tắc thiết bị, rút cắm lại receiver/cáp USB. Với chuột quang, kiểm tra đèn cảm biến.

### Bước 2: Thử cổng khác

Cắm trực tiếp vào laptop hoặc PC, tránh hub/dock để loại trừ lỗi trung gian. Nếu hoạt động, kiểm tra hub/dock.

### Bước 3: Xử lý Bluetooth

Settings > Bluetooth & devices: tắt bật Bluetooth, remove thiết bị, pair lại. Đảm bảo thiết bị ở chế độ pairing.

### Bước 4: Kiểm tra Device Manager

Device Manager > Keyboards, Mice and other pointing devices, Human Interface Devices. Nếu có dấu chấm than, gỡ thiết bị rồi Scan for hardware changes.

### Bước 5: Kiểm tra accessibility

Settings > Accessibility > Keyboard/Mouse: tắt Filter Keys, Sticky Keys hoặc Mouse Keys nếu người dùng không dùng các tính năng này.

## Khi nào chuyển cấp (escalate)

- Bàn phím laptop tích hợp không hoạt động cả trong BIOS.
- Nhiều cổng USB cùng lỗi.
- Thiết bị thuộc bộ chuyên dụng cần driver hoặc phần mềm riêng.

**Thông tin đính kèm ticket:** loại thiết bị, cách kết nối, kết quả thử trên máy khác, ảnh Device Manager.

## Phòng ngừa

- Dự phòng pin và bộ bàn phím/chuột thay thế.
- Ghi nhãn receiver theo thiết bị.
- Hạn chế dùng hub USB kém chất lượng.

## Mẫu ghi chú đóng ticket

> Nguyên nhân: USB receiver cắm qua hub lỗi. Cách xử lý: cắm receiver trực tiếp vào laptop, thiết bị hoạt động ổn định.

