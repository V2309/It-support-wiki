# Outlook không gửi hoặc nhận được thư

| | |
| --- | --- |
| Cấp độ | L1 / L2 |
| Thời gian xử lý ước tính | 15-35 phút |
| Cần quyền quản trị | Có nếu kiểm tra mailbox hoặc license |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Email kẹt trong Outbox.
- Không nhận thư mới nhưng Outlook Web vẫn nhận được.
- Outlook báo "Disconnected", "Trying to connect" hoặc yêu cầu nhập mật khẩu liên tục.

## Câu hỏi cần hỏi người dùng trước

- Outlook desktop lỗi hay cả Outlook Web?
- Lỗi với mọi email hay chỉ email có file đính kèm?
- Mailbox có gần đầy không?

## Nguyên nhân thường gặp

1. Mất mạng hoặc Outlook mất kết nối Exchange.
2. Chế độ Work Offline đang bật.
3. File OST hoặc profile Outlook lỗi.
4. Mailbox đầy hoặc file đính kèm quá lớn.
5. License hoặc tài khoản Microsoft 365 có vấn đề.

## Các bước xử lý

### Bước 1: Kiểm tra Outlook Web

Truy cập `https://outlook.office.com`. Nếu web cũng lỗi, kiểm tra tài khoản Microsoft 365 theo bài [Không đăng nhập được Microsoft 365](07-khong-dang-nhap-duoc-microsoft-365.md).

### Bước 2: Tắt Work Offline

Trong Outlook: Send/Receive > đảm bảo **Work Offline** không được bật. Bấm **Update Folder** hoặc **Send/Receive All Folders**.

### Bước 3: Kiểm tra Outbox và dung lượng

Xóa hoặc mở email kẹt trong Outbox, giảm dung lượng file đính kèm. Kiểm tra mailbox quota trong Outlook hoặc admin center.

### Bước 4: Chạy Outlook Safe Mode

```cmd
outlook.exe /safe
```

Nếu chạy được, tắt add-in không cần thiết trong File > Options > Add-ins.

### Bước 5: Tạo lại profile Outlook

Control Panel > Mail > Show Profiles > Add. Tạo profile mới và đặt làm mặc định. Không xóa profile cũ cho đến khi xác nhận dữ liệu đã đồng bộ.

## Khi nào chuyển cấp (escalate)

- Outlook Web cũng không gửi/nhận được.
- Nhiều người cùng lỗi Exchange/Microsoft 365.
- Mailbox bị litigation hold, retention hoặc policy đặc biệt.

**Thông tin đính kèm ticket:** ảnh lỗi, Outlook desktop/web, mailbox quota, thời điểm lỗi, email kẹt nếu có.

## Phòng ngừa

- Hướng dẫn lưu file lớn trên OneDrive thay vì đính kèm.
- Giám sát mailbox gần đầy.
- Hạn chế add-in Outlook không cần thiết.

## Mẫu ghi chú đóng ticket

> Nguyên nhân: profile Outlook bị lỗi, Outlook Web vẫn hoạt động. Cách xử lý: tạo profile Outlook mới, đồng bộ mailbox và gửi nhận thử thành công.

