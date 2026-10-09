# Outlook không gửi hoặc nhận được thư

| | |
| --- | --- |
| Cấp độ | L1 / L2 |
| Mức ưu tiên thường gặp | P3; P2 nếu ảnh hưởng nhiều người hoặc tài khoản lãnh đạo |
| Thời gian xử lý ước tính | 15-35 phút |
| Cần quyền quản trị | Có nếu kiểm tra mailbox hoặc license |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Email kẹt trong Outbox không gửi đi được.
- Không nhận thư mới nhưng Outlook Web vẫn nhận được bình thường.
- Góc dưới thanh trạng thái Outlook báo "Disconnected", "Trying to connect" hoặc liên tục hiện pop-up đòi nhập mật khẩu (Need Password).

## Câu hỏi cần hỏi người dùng trước

- Outlook desktop lỗi hay cả Outlook Web?
- Lỗi với mọi email hay chỉ email có file đính kèm dung lượng lớn?
- Hòm thư (Mailbox) có thông báo gần đầy dung lượng không?
- Bạn có vừa đổi mật khẩu tài khoản gần đây không?

## Kiểm tra nhanh

- Nhìn góc dưới cùng bên phải của cửa sổ Outlook xem trạng thái kết nối đang là: **Connected to: Microsoft Exchange**, **Disconnected**, hay **Need Password**.
- Hướng dẫn người dùng đăng nhập ngay vào Outlook Web (`https://outlook.office.com`) để gửi nhận thư tạm thời trong lúc xử lý app.
- Kiểm tra dung lượng hòm thư trong File > Info xem thanh dung lượng có bị chạm vạch đỏ (Full quota) không.

## Nguyên nhân thường gặp

1. Mất mạng hoặc Outlook mất kết nối Exchange.
2. Chế độ Work Offline đang bật vô tình.
3. Cache token xác thực Modern Authentication (WAM Broker) bị lỗi sau khi đổi mật khẩu.
4. File dữ liệu OST hoặc profile Outlook bị lỗi phân mảnh.
5. Mailbox đầy hoặc file đính kèm vượt quá giới hạn server (thường > 25MB-35MB).
6. License hoặc tài khoản Microsoft 365 có vấn đề.

## Các bước xử lý

### Bước 1: Kiểm tra Outlook Web

Truy cập `https://outlook.office.com`. Nếu web cũng lỗi, kiểm tra tài khoản Microsoft 365 theo bài [Không đăng nhập được Microsoft 365](07-khong-dang-nhap-duoc-microsoft-365.md).

### Bước 2: Tắt chế độ Work Offline

Trong Outlook: Chọn tab **Send / Receive** > Đảm bảo nút **Work Offline** không sáng màu (không được bật). Bấm nút **Send/Receive All Folders** để kích hoạt đồng bộ.

### Bước 3: Sửa lỗi pop-up đòi mật khẩu (Modern Authentication / Token Cache)

Nếu Outlook liên tục nháy pop-up đăng nhập hoặc báo Need Password nhưng không cho nhập:
1. Đóng hoàn toàn Outlook.
2. Mở **Control Panel** > **Credential Manager** > **Windows Credentials**: Tìm và xóa (Remove) tất cả các dòng có chữ `MicrosoftOffice16_Data` và `adal`.
3. Vào **Windows Settings** > **Accounts** > **Access work or school**: Nếu thấy tài khoản công ty, bấm **Disconnect**, sau đó mở lại Outlook để đăng nhập và cấp quyền lại.

### Bước 4: Kiểm tra thư mục Outbox và file đính kèm

Vào thư mục **Outbox**: Nếu có email đang bị kẹt, chuyển Outlook sang chế độ Work Offline tạm thời, kéo email kẹt ra thư mục Drafts hoặc xóa bỏ. Giảm dung lượng file đính kèm (hoặc upload qua OneDrive/SharePoint và gửi link chia sẻ).

### Bước 5: Khởi động Outlook ở chế độ Safe Mode

```cmd
outlook.exe /safe
```

Nếu chạy bình thường ở Safe Mode, lỗi do Add-in gây xung đột: Vào **File** > **Options** > **Add-ins** > Mục Manage chọn **COM Add-ins** > Bấm **Go** > Bỏ chọn các add-in không cần thiết (đặc biệt là add-in của phần mềm diệt virus bên thứ ba).

### Bước 6: Đổi tên file OST hoặc tạo lại Profile Outlook

> [!WARNING]
> Luôn giữ lại file dữ liệu lưu trữ cá nhân (.pst) nếu có trước khi can thiệp profile.

Nếu file đồng bộ `.ost` bị hỏng:
1. Đóng Outlook.
2. Mở hộp thoại Run (`Win + R`), gõ:
   ```cmd
   %localappdata%\Microsoft\Outlook
   ```
3. Đổi tên file `<email>.ost` thành `<email>.ost.old`.
4. Mở lại Outlook, ứng dụng sẽ tự động tải lại hòm thư mới từ Exchange Server.
5. Nếu vẫn không được: Vào Control Panel > **Mail (Microsoft Outlook)** > **Show Profiles** > Bấm **Add** để tạo Profile mới.

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

