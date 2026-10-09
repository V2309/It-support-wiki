# Quên mật khẩu

| | |
| --- | --- |
| Cấp độ | L1 |
| Thời gian xử lý ước tính | 5-10 phút |
| Cần quyền quản trị | Có (đặt lại mật khẩu cho người khác) |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Người dùng không nhớ mật khẩu Windows, Microsoft 365 hoặc ứng dụng nội bộ.
- Báo "The user name or password is incorrect" hoặc tài khoản bị khóa sau nhiều lần nhập sai.

## Nguyên tắc bảo mật (đọc trước khi làm)

Yêu cầu đặt lại mật khẩu là một trong những cách phổ biến để kẻ tấn công chiếm tài khoản. Vì vậy:

1. **Luôn xác minh danh tính** trước khi đặt lại.
2. **Không bao giờ hỏi mật khẩu cũ** của người dùng.
3. **Không gửi mật khẩu mới qua chat hoặc email thường.** Đọc qua điện thoại sau khi đã xác minh, hoặc dùng kênh được công ty phê duyệt.
4. **Bắt buộc đổi mật khẩu ở lần đăng nhập đầu tiên.**
5. Ghi lại trong ticket: ai yêu cầu, cách xác minh, thời điểm đặt lại.

## Cách xác minh danh tính

Dùng ít nhất hai yếu tố, theo quy định của công ty, ví dụ:

- Mã nhân viên và ngày vào làm hoặc thông tin trong hồ sơ nhân sự.
- Gọi lại vào số điện thoại đã đăng ký trong hệ thống (không gọi vào số người yêu cầu đưa).
- Quản lý trực tiếp xác nhận bằng kênh nội bộ đáng tin cậy.
- Người dùng có mặt trực tiếp và xuất trình thẻ nhân viên.

Nếu không xác minh được, từ chối đặt lại và chuyển cho quản lý hoặc nhóm bảo mật.

## Các bước xử lý

### Cách 1 (ưu tiên): Tự đặt lại mật khẩu (Self-Service Password Reset)

Nếu công ty đã bật SSPR cho Microsoft 365 / Entra ID:

1. Người dùng vào trang đặt lại mật khẩu của Microsoft (`https://aka.ms/sspr`).
2. Nhập email công ty, làm theo xác thực bằng điện thoại hoặc ứng dụng Authenticator.
3. Đặt mật khẩu mới theo chính sách.

**Ưu điểm:** không cần Helpdesk can thiệp, giảm rủi ro lộ mật khẩu.

Nếu người dùng chưa đăng ký phương thức xác thực cho SSPR, chuyển sang Cách 2.

### Cách 2: Helpdesk đặt lại bằng giao diện Active Directory

1. Mở **Active Directory Users and Computers**.
2. Tìm tài khoản (chuột phải > Find).
3. Chuột phải tài khoản > **Reset Password**.
4. Nhập mật khẩu tạm thời mạnh, chọn **User must change password at next logon**.
5. Nếu tài khoản đang bị khóa, chọn **Unlock the user's account**.
6. Bấm OK.

### Cách 3: Helpdesk đặt lại bằng PowerShell (cần quyền quản trị)

```powershell
# Thay "ten.nguoidung" bằng tên đăng nhập thực tế
$mk = Read-Host -AsSecureString "Nhập mật khẩu tạm thời"
Set-ADAccountPassword -Identity "ten.nguoidung" -Reset -NewPassword $mk
Set-ADUser -Identity "ten.nguoidung" -ChangePasswordAtLogon $true
Unlock-ADAccount -Identity "ten.nguoidung"
```

Dùng `Read-Host -AsSecureString` để mật khẩu không hiện trên màn hình và không bị lưu trong lịch sử lệnh.

### Cách 4: Tài khoản Microsoft 365 (không đồng bộ từ AD)

Trong Microsoft 365 admin center: Users > Active users > chọn người dùng > **Reset password**. Chọn bắt buộc đổi mật khẩu ở lần đăng nhập sau.

## Sau khi đặt lại

- Hướng dẫn người dùng đăng nhập và đổi sang mật khẩu của riêng họ.
- Nhắc người dùng cập nhật mật khẩu đã lưu trên điện thoại (email, Wi-Fi công ty), vì thiết bị cũ có thể tiếp tục thử mật khẩu cũ và làm khóa tài khoản lại.
- Đề nghị đăng ký SSPR và MFA nếu chưa có.

## Khi nào chuyển cấp (escalate)

- Không xác minh được danh tính, hoặc có dấu hiệu bất thường (người lạ yêu cầu gấp, tìm cách bỏ qua quy trình).
- Tài khoản quản trị hoặc tài khoản đặc quyền.
- Tài khoản bị khóa lặp lại nhiều lần (có thể có thiết bị đang dùng mật khẩu cũ hoặc nghi bị tấn công dò mật khẩu).
- Người dùng nghi ngờ tài khoản đã bị lộ.

## Phòng ngừa

- Bật SSPR và MFA cho toàn bộ nhân viên.
- Dùng trình quản lý mật khẩu được công ty phê duyệt.
- Hướng dẫn mật khẩu dài (cụm từ) thay vì mật khẩu ngắn phức tạp.

## Mẫu ghi chú đóng ticket

> Người dùng quên mật khẩu Windows. Đã xác minh danh tính qua mã nhân viên và gọi lại số điện thoại đã đăng ký. Đặt lại mật khẩu tạm thời, bắt buộc đổi ở lần đăng nhập đầu. Đã hướng dẫn đăng ký SSPR.
