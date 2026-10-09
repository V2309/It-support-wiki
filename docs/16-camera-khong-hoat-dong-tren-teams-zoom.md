# Camera không hoạt động trên Teams/Zoom

| | |
| --- | --- |
| Cấp độ | L1 |
| Mức ưu tiên thường gặp | P3; P2 nếu trong cuộc họp khẩn với đối tác hoặc ban lãnh đạo |
| Thời gian xử lý ước tính | 10-20 phút |
| Cần quyền quản trị | Không, trừ khi cài driver |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Teams/Zoom báo không tìm thấy camera.
- Camera đen, mờ hoặc đang bị ứng dụng khác sử dụng.
- Đèn camera không bật khi vào cuộc họp.

## Câu hỏi cần hỏi người dùng trước

- Camera tích hợp hay webcam rời?
- Camera có hoạt động trong ứng dụng Camera của Windows không?
- Có nắp che camera hoặc phím tắt privacy không?

## Kiểm tra nhanh

- Kiểm tra cần gạt / nắp che vật lý (Privacy shutter) phía trước ống kính webcam laptop.
- Kiểm tra các phím chức năng (thường là `F8`, `F10` hoặc `Fn + phím camera`) trên laptop Asus, Lenovo, MSI, HP có đang tắt camera ở cấp độ phần cứng không.
- Mở nhanh ứng dụng **Camera** có sẵn của Windows (Start > gõ "Camera") xem có xuất hiện hình ảnh không.

## Nguyên nhân thường gặp

1. Camera bị che hoặc tắt bằng phím privacy.
2. Ứng dụng khác đang chiếm camera.
3. Quyền camera trong Windows bị tắt.
4. Chọn sai camera trong Teams/Zoom.
5. Driver camera lỗi.

## Các bước xử lý

### Bước 1: Kiểm tra vật lý và ứng dụng Camera

Mở ứng dụng **Camera** của Windows. Nếu không có hình, kiểm tra nắp che, phím camera trên bàn phím, công tắc privacy.

### Bước 2: Kiểm tra quyền camera

Settings > Privacy & security > Camera, bật quyền truy cập camera cho thiết bị và desktop apps.

### Bước 3: Chọn đúng camera trong Teams/Zoom

Vào Settings > Video, chọn đúng camera. Tắt các ứng dụng khác có thể dùng camera như trình duyệt, phần mềm quay màn hình.

### Bước 4: Khởi động lại ứng dụng và máy

Thoát hẳn Teams/Zoom ở khay hệ thống, mở lại. Nếu vẫn lỗi, khởi động lại máy.

### Bước 5: Kiểm tra driver

Device Manager > Cameras. Nếu có dấu chấm than, cập nhật driver hoặc gỡ thiết bị rồi Scan for hardware changes.

## Khi nào chuyển cấp (escalate)

- Camera không hoạt động cả trong BIOS/diagnostic hoặc ứng dụng Camera.
- Webcam rời lỗi trên nhiều máy.
- Chính sách bảo mật đang chặn camera.

**Thông tin đính kèm ticket:** model máy/webcam, app bị lỗi, ảnh Device Manager, kết quả test Camera app.

## Phòng ngừa

- Cấp webcam chuẩn cho máy không có camera tốt.
- Hướng dẫn kiểm tra camera trước cuộc họp.
- Cập nhật driver theo chuẩn thiết bị.

## Mẫu ghi chú đóng ticket

> Nguyên nhân: quyền camera cho desktop apps bị tắt. Cách xử lý: bật lại quyền trong Windows, chọn đúng camera trong Teams, video hoạt động bình thường.

