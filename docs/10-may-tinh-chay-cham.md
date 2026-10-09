# Máy tính chạy chậm

| | |
| --- | --- |
| Cấp độ | L1 |
| Thời gian xử lý ước tính | 20-45 phút |
| Cần quyền quản trị | Có nếu gỡ phần mềm hoặc thay đổi startup |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Máy khởi động lâu, mở ứng dụng chậm, quạt chạy mạnh.
- CPU, RAM hoặc disk luôn gần 100%.
- Ứng dụng Office, trình duyệt hoặc phần mềm nội bộ hay treo.

## Câu hỏi cần hỏi người dùng trước

- Máy chậm từ khi nào? Chậm mọi lúc hay chỉ khi mở ứng dụng nào?
- Có vừa cài phần mềm, cập nhật Windows hoặc mở file lạ không?
- Máy dùng HDD hay SSD, RAM bao nhiêu?

## Nguyên nhân thường gặp

1. Quá nhiều chương trình khởi động cùng Windows.
2. Thiếu RAM hoặc ổ đĩa gần đầy.
3. Windows Update, antivirus scan hoặc OneDrive sync đang chạy.
4. Ổ HDD lỗi hoặc quá chậm.
5. Nghi nhiễm mã độc.

## Các bước xử lý

### Bước 1: Kiểm tra Task Manager

Mở Task Manager > Processes, sắp xếp theo CPU, Memory, Disk để tìm tiến trình chiếm tài nguyên.

Nếu tiến trình là antivirus hoặc Windows Update, chờ hoàn tất nếu đang chạy hợp lệ. Nếu là ứng dụng lạ, ghi lại tên và chuyển sang kiểm tra mã độc.

### Bước 2: Kiểm tra dung lượng ổ đĩa

Settings > System > Storage. Đảm bảo ổ C còn ít nhất 15-20% dung lượng trống.

Chạy Disk Cleanup hoặc Storage Sense để xóa file tạm. Không xóa thư mục người dùng nếu chưa sao lưu.

### Bước 3: Tắt startup không cần thiết

Task Manager > Startup apps, tắt ứng dụng không cần chạy cùng Windows như updater phụ, chat cá nhân, launcher không dùng.

### Bước 4: Kiểm tra sức khỏe ổ đĩa

```cmd
wmic diskdrive get status
chkdsk C: /scan
```

Nếu báo lỗi ổ đĩa hoặc máy dùng HDD quá chậm, đề xuất thay SSD hoặc chuyển bảo hành.

### Bước 5: Quét mã độc

Chạy Microsoft Defender hoặc công cụ EDR của công ty. Nếu phát hiện file lạ hoặc popup bất thường, xử lý theo [Máy có popup lạ, nghi nhiễm mã độc](20-may-co-popup-la-nghi-nhiem-ma-doc.md).

## Khi nào chuyển cấp (escalate)

- Disk 100% liên tục dù không chạy ứng dụng nặng.
- Ổ đĩa báo lỗi hoặc có dấu hiệu sắp hỏng.
- Nghi nhiễm mã độc hoặc tiến trình lạ không xử lý được.

**Thông tin đính kèm ticket:** model máy, RAM, loại ổ, ảnh Task Manager, tiến trình chiếm tài nguyên.

## Phòng ngừa

- Chuẩn hóa cấu hình tối thiểu: SSD, RAM đủ cho vai trò công việc.
- Quản lý startup app bằng chính sách thiết bị.
- Dọn dung lượng và cập nhật định kỳ.

## Mẫu ghi chú đóng ticket

> Nguyên nhân: ổ C gần đầy và nhiều ứng dụng khởi động cùng Windows. Cách xử lý: dọn file tạm, tắt startup không cần thiết, khởi động lại, máy phản hồi bình thường.

