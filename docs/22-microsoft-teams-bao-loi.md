# Microsoft Teams báo lỗi, kẹt đăng nhập hoặc trắng màn hình

| | |
| --- | --- |
| Cấp độ | L1 |
| Mức ưu tiên thường gặp | P3; P2 nếu nhiều người dùng trong công ty không họp hoặc nhắn tin được |
| Thời gian xử lý ước tính | 10-25 phút |
| Cần quyền quản trị | Không (hầu hết thao tác trên tài khoản người dùng) |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Teams mở lên bị kẹt ở màn hình "Loading Microsoft Teams..." hoặc màn hình trắng xóa/đen sì.
- Báo lỗi đăng nhập mã: `CAA70004`, `CAA20003`, `80090016` hoặc `80090030`.
- Đăng nhập liên tục bị đẩy văng ra màn hình chọn tài khoản.
- Không chia sẻ được màn hình hoặc không load được lịch họp/tin nhắn.

## Câu hỏi cần hỏi người dùng trước

- Đang dùng New Teams (Teams mới có chữ "NEW" trên icon) hay Classic Teams?
- Đăng nhập Teams trên trình duyệt web (`https://teams.microsoft.com`) có bình thường không?
- Bạn có vừa đổi mật khẩu tài khoản Microsoft 365 không?
- Sự cố chỉ bị trên máy này hay trên điện thoại cũng bị?

## Kiểm tra nhanh

- Yêu cầu người dùng truy cập `https://teams.microsoft.com` qua trình duyệt Edge/Chrome để xác nhận tài khoản và license M365 vẫn hoạt động bình thường.
- Kiểm tra kết nối mạng và tắt VPN tạm thời nếu đang bật.
- Tắt hoàn toàn Teams qua Task Manager (End task mọi tiến trình `ms-teams.exe` hoặc `Teams.exe`).

## Nguyên nhân thường gặp

1. Cache và token xác thực của Teams bị hỏng hoặc xung đột sau khi đổi mật khẩu.
2. Xung đột tài khoản xác thực Windows (Work or School Account / WAM Broker).
3. Bản cài đặt Teams bị lỗi sau khi Windows Update.
4. Lỗi phần cứng tăng tốc đồ họa (Hardware Acceleration).
5. Tài khoản bị vô hiệu hóa license Microsoft Teams.

## Các bước xử lý

### Bước 1: Kiểm tra trên Teams Web

Mở trình duyệt truy cập:
```text
https://teams.microsoft.com
```
- **Kết quả mong đợi:** Nếu vào bình thường → Xác định lỗi do ứng dụng Teams Desktop trên máy, tiếp tục Bước 2.
- **Nếu web cũng không vào được:** Kiểm tra license và trạng thái tài khoản M365 theo bài [Không đăng nhập được Microsoft 365](07-khong-dang-nhap-duoc-microsoft-365.md).

### Bước 2: Tắt tận gốc tiến trình Teams

Nhấn `Ctrl + Shift + Esc` mở **Task Manager** > Tìm tất cả các tiến trình có tên **Microsoft Teams** > Bấm **End task**.

Hoặc chạy nhanh lệnh qua Command Prompt:
```cmd
taskkill /f /im ms-teams.exe
taskkill /f /im teams.exe
```

### Bước 3: Xóa cache Microsoft Teams

Tùy vào phiên bản Teams máy đang sử dụng:

#### Với New Teams (bản mặc định hiện nay trên Windows 11 / M365):
1. Vào **Settings** (Windows) > **Apps** > **Installed apps**.
2. Tìm **Microsoft Teams** (biểu tượng có chữ NEW).
3. Bấm vào dấu ba chấm `...` > Chọn **Advanced options**.
4. Cuộn xuống mục Reset:
   - Thử bấm nút **Repair** trước (không mất dữ liệu cấu hình).
   - Nếu không được, bấm nút **Reset**.

Hoặc xóa cache bằng lệnh PowerShell:
```powershell
Remove-Item -Path "$env:LOCALAPPDATA\Packages\MSTeams_8wekyb3d8bbwe\LocalCache\Microsoft\MSTeams\*" -Recurse -Force -ErrorAction SilentlyContinue
```

#### Với Classic Teams (bản cũ):
Mở hộp thoại Run (`Win + R`), dán lệnh sau và nhấn Enter:
```cmd
%appdata%\Microsoft\Teams
```
Xóa toàn bộ các file và thư mục bên trong thư mục này, sau đó mở lại Teams.

### Bước 4: Làm mới liên kết tài khoản trong Windows

Nếu Teams báo lỗi `80090016` hoặc kẹt vòng lặp đăng nhập:
1. Vào **Settings** > **Accounts** > **Access work or school**.
2. Tìm tài khoản công ty đang đăng nhập > Bấm **Disconnect** (Ngắt kết nối).
3. Khởi động lại máy.
4. Mở lại Teams và đăng nhập lại, chọn *"Allow my organization to manage my device"*.

### Bước 5: Cài đặt lại Microsoft Teams

Nếu các bước trên không hiệu quả:
1. Vào Settings > Apps > Gỡ cài đặt Microsoft Teams.
2. Tải bản New Teams mới nhất từ trang chính thức:
   ```text
   https://www.microsoft.com/en-us/microsoft-teams/download-app
   ```
3. Cài đặt lại và đăng nhập.

## Khi nào chuyển cấp (escalate)

- Nhiều người dùng trong công ty cùng bị lỗi không đăng nhập được Teams hoặc dịch vụ Teams toàn cầu bị gián đoạn (kiểm tra Service Health trên Microsoft 365 admin center).
- Tài khoản bị lỗi Conditional Access chặn truy cập hoặc thiết bị không đáp ứng tiêu chuẩn Intune Compliance.

**Thông tin đính kèm ticket:** Mã lỗi hiển thị (ảnh chụp), phiên bản Teams (New hay Classic), kết quả test trên Teams Web, tài khoản người dùng.

## Phòng ngừa

- Hướng dẫn người dùng đăng xuất và đăng nhập lại Teams ngay sau khi đổi mật khẩu tài khoản công ty.
- Khuyến khích sử dụng New Teams để được cập nhật bản vá bảo mật và hiệu năng tốt hơn.

## Mẫu ghi chú đóng ticket

> Nguyên nhân: New Teams bị lỗi cache token xác thực sau khi người dùng đổi mật khẩu. Cách xử lý: đóng triệt để tiến trình Teams trong Task Manager, reset app trong Windows Settings > Installed apps, hỗ trợ người dùng đăng nhập lại thành công. Đã test gọi và nhắn tin bình thường.
