# Windows Update báo lỗi

| | |
| --- | --- |
| Cấp độ | L1 / L2 |
| Thời gian xử lý ước tính | 20-45 phút |
| Cần quyền quản trị | Có |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Windows Update tải hoặc cài đặt thất bại.
- Máy khởi động lại nhiều lần nhưng vẫn báo pending update.
- Mã lỗi như `0x80070002`, `0x80070005`, `0x8024a105`.

## Câu hỏi cần hỏi người dùng trước

- Mã lỗi chính xác là gì?
- Máy có đủ dung lượng ổ C không?
- Máy đang dùng mạng công ty, VPN hay mạng ngoài?

## Nguyên nhân thường gặp

1. Thiếu dung lượng ổ đĩa.
2. Cache Windows Update hỏng.
3. Dịch vụ update bị dừng.
4. Chính sách WSUS/Intune chưa đồng bộ.
5. File hệ thống Windows lỗi.

## Các bước xử lý

### Bước 1: Kiểm tra dung lượng và khởi động lại

Đảm bảo ổ C còn ít nhất 15-20 GB trống cho feature update. Khởi động lại máy và thử update lại.

### Bước 2: Chạy troubleshooter

Settings > System > Troubleshoot > Other troubleshooters > Windows Update > Run.

### Bước 3: Kiểm tra dịch vụ

Mở Command Prompt quyền quản trị:

```cmd
sc query wuauserv
sc query bits
```

Nếu dịch vụ dừng, thử khởi động:

```cmd
net start wuauserv
net start bits
```

### Bước 4: Reset cache Windows Update

```cmd
net stop wuauserv
net stop bits
ren C:\Windows\SoftwareDistribution SoftwareDistribution.old
net start bits
net start wuauserv
```

Sau đó kiểm tra update lại.

### Bước 5: Kiểm tra file hệ thống

```cmd
sfc /scannow
DISM /Online /Cleanup-Image /RestoreHealth
```

## Khi nào chuyển cấp (escalate)

- Máy thuộc vòng cập nhật do WSUS/Intune quản lý và nhiều máy cùng lỗi.
- Update liên tục rollback sau restart.
- DISM/SFC không sửa được lỗi hệ thống.

**Thông tin đính kèm ticket:** mã lỗi, ảnh Windows Update, dung lượng ổ C, kết quả SFC/DISM, chính sách update áp dụng.

## Phòng ngừa

- Theo dõi thiết bị quá hạn update.
- Giữ đủ dung lượng ổ C.
- Thử update theo vòng pilot trước khi triển khai rộng.

## Mẫu ghi chú đóng ticket

> Nguyên nhân: cache Windows Update hỏng. Cách xử lý: reset thư mục SoftwareDistribution, chạy lại update, cài đặt bản cập nhật thành công.

