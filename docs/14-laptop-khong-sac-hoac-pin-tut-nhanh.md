# Laptop không sạc hoặc pin tụt nhanh

| | |
| --- | --- |
| Cấp độ | L1 / L2 |
| Mức ưu tiên thường gặp | P3; P2 nếu máy sập nguồn không thể bật khi cần làm việc khẩn |
| Thời gian xử lý ước tính | 15-30 phút |
| Cần quyền quản trị | Không, trừ khi cập nhật BIOS/firmware |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Cắm sạc nhưng pin không tăng hoặc báo "Plugged in, not charging".
- Máy sập nguồn khi rút sạc.
- Pin tụt nhanh bất thường.

## Câu hỏi cần hỏi người dùng trước

- Dùng sạc gốc, dock USB-C hay sạc khác?
- Có thông báo adapter watt thấp không?
- Pin tụt nhanh từ khi nào? Có chạy ứng dụng nặng hay họp video liên tục không?

## Kiểm tra nhanh

- Kiểm tra đèn LED chỉ báo sạc cạnh cổng cắm nguồn (sáng trắng/cam hay nhấp nháy/tắt hẳn).
- Cầm thử củ sạc (adapter) xem có ấm không (nếu nguội hoàn toàn là sạc hỏng hoặc mất nguồn điện ổ cắm).
- Chạy nhanh lệnh xuất báo cáo độ chai pin:
  ```cmd
  powercfg /batteryreport /output C:\battery-report.html
  ```
  Mở file html đối chiếu **Design Capacity** (dung lượng thiết kế) và **Full Charge Capacity** (dung lượng thực tế hiện tại).

## Nguyên nhân thường gặp

1. Adapter, cáp sạc hoặc ổ điện lỗi.
2. Cổng sạc lỏng hoặc bẩn.
3. Sạc USB-C không đủ công suất.
4. Pin chai hoặc lỗi.
5. BIOS/firmware quản lý pin lỗi.

## Các bước xử lý

### Bước 1: Kiểm tra sạc và nguồn điện

Thử ổ điện khác, kiểm tra đèn adapter, dùng sạc đúng công suất. Với USB-C, dùng cổng có biểu tượng sạc nếu máy có nhiều cổng.

### Bước 2: Khởi động lại và xả điện tĩnh

Tắt máy, rút sạc, giữ nút nguồn 15-30 giây, cắm sạc lại và bật máy.

### Bước 3: Kiểm tra báo cáo pin

```cmd
powercfg /batteryreport
```

Mở file HTML được tạo và so sánh **Design Capacity** với **Full Charge Capacity**. Nếu dung lượng còn quá thấp, đề xuất thay pin.

### Bước 4: Kiểm tra ứng dụng tiêu thụ pin

Settings > System > Power & battery > Battery usage, xem ứng dụng nào dùng nhiều pin. Tắt ứng dụng nền không cần thiết.

### Bước 5: Cập nhật firmware nếu cần

Dùng công cụ chính hãng như Dell Command Update, Lenovo Vantage hoặc HP Support Assistant theo chuẩn công ty.

## Khi nào chuyển cấp (escalate)

- Pin phồng, máy nóng bất thường hoặc có mùi khét: ngừng sử dụng ngay.
- Adapter hoặc cổng sạc nghi hỏng.
- Pin chai cần thay thế bảo hành.

**Thông tin đính kèm ticket:** model máy, serial, loại sạc, ảnh thông báo lỗi, battery report.

## Phòng ngừa

- Cấp sạc đúng công suất.
- Không dùng sạc USB-C không rõ nguồn gốc.
- Theo dõi pin chai trong vòng đời thiết bị.

## Mẫu ghi chú đóng ticket

> Nguyên nhân: người dùng dùng sạc USB-C 30W không đủ công suất. Cách xử lý: thay sạc 65W chuẩn của hãng, máy nhận sạc và pin tăng bình thường.

