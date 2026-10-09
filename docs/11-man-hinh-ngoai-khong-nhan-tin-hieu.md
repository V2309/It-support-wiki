# Màn hình ngoài không nhận tín hiệu

| | |
| --- | --- |
| Cấp độ | L1 |
| Mức ưu tiên thường gặp | P3; P2 nếu là màn hình máy chiếu/TV phòng họp khẩn |
| Thời gian xử lý ước tính | 10-25 phút |
| Cần quyền quản trị | Không, trừ khi cài driver |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Màn hình ngoài báo "No signal".
- Windows không phát hiện màn hình thứ hai.
- Hình nhấp nháy, sai độ phân giải hoặc chỉ hiện trên laptop.

## Câu hỏi cần hỏi người dùng trước

- Dùng cáp HDMI, DisplayPort, USB-C hay dock?
- Màn hình và cáp này có hoạt động với máy khác không?
- Lỗi xảy ra sau khi đổi dock, đổi bàn làm việc hoặc cập nhật driver không?

## Kiểm tra nhanh

- Bấm tổ hợp phím `Win + P` và chọn **Duplicate** hoặc **Extend** (đảm bảo không bị kẹt ở "PC screen only").
- Bấm phím tắt khởi động lại driver card màn hình: `Win + Ctrl + Shift + B` (màn hình sẽ chớp nhẹ một lần).
- Kiểm tra đèn LED nguồn trên màn hình ngoài và đảm bảo dock sạc đã cắm nguồn điện AC riêng.

## Nguyên nhân thường gặp

1. Chọn sai nguồn vào trên màn hình.
2. Cáp hoặc adapter lỗi.
3. Dock chưa nhận nguồn hoặc firmware lỗi.
4. Windows đang ở chế độ chỉ màn hình laptop.
5. Driver đồ họa lỗi.

## Các bước xử lý

### Bước 1: Kiểm tra nguồn vào và cáp

Đảm bảo màn hình bật nguồn, chọn đúng input. Rút cắm lại hai đầu cáp, thử cáp hoặc cổng khác nếu có.

### Bước 2: Chọn chế độ hiển thị

Nhấn `Windows + P`, chọn **Duplicate** hoặc **Extend**. Sau đó vào Settings > System > Display, bấm **Detect**.

### Bước 3: Kiểm tra dock và USB-C

- Rút nguồn dock 30 giây rồi cắm lại.
- Cắm laptop trực tiếp vào màn hình để loại trừ dock.
- Kiểm tra cổng USB-C có hỗ trợ xuất hình hay chỉ truyền dữ liệu.

### Bước 4: Kiểm tra độ phân giải và tần số quét

Settings > Display > Advanced display, đặt độ phân giải khuyến nghị và refresh rate phổ biến như 60 Hz.

### Bước 5: Cập nhật driver

Cập nhật driver đồ họa và firmware dock theo gói chuẩn của hãng hoặc công ty.

## Khi nào chuyển cấp (escalate)

- Cổng xuất hình của laptop nghi hỏng.
- Dock lỗi hàng loạt hoặc cần cập nhật firmware tập trung.
- Màn hình có lỗi phần cứng.

**Thông tin đính kèm ticket:** model laptop, dock, màn hình, loại cáp, kết quả thử cáp/máy khác.

## Phòng ngừa

- Chuẩn hóa dock và cáp đạt chuẩn.
- Ghi nhãn nguồn vào màn hình tại bàn làm việc.
- Cập nhật firmware dock theo đợt.

## Mẫu ghi chú đóng ticket

> Nguyên nhân: màn hình đang chọn sai input. Cách xử lý: chuyển input sang HDMI 1, đặt Windows ở chế độ Extend, màn hình ngoài hoạt động bình thường.

