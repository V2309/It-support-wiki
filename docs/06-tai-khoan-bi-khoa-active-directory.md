# Tài khoản bị khóa (Active Directory)

| | |
| --- | --- |
| Cấp độ | L1 / L2 |
| Mức ưu tiên thường gặp | P3; P2 nếu tài khoản quản lý/VIP hoặc bị khóa hàng loạt |
| Thời gian xử lý ước tính | 10-30 phút |
| Cần quyền quản trị | Có |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Người dùng nhập đúng mật khẩu nhưng Windows hoặc Microsoft 365 báo tài khoản bị khóa.
- Tài khoản vừa mở khóa lại bị khóa sau vài phút.
- Event log ghi nhiều lần đăng nhập sai.

## Câu hỏi cần hỏi người dùng trước

- Gần đây có đổi mật khẩu không?
- Có dùng email trên điện thoại, Outlook cũ, VPN, Wi-Fi công ty hoặc ứng dụng lưu mật khẩu không?
- Tài khoản bị khóa một lần hay lặp lại liên tục?

## Kiểm tra nhanh

- Xác minh trạng thái khóa tài khoản trên Active Directory (`Get-ADUser -Identity "ten.nguoidung" -Properties LockedOut`).
- Kiểm tra xem người dùng có đăng nhập trên nhiều thiết bị cùng lúc (điện thoại, laptop thứ hai, máy ảo).
- Xác định tài khoản cá nhân hay tài khoản quản trị viên.

## Nguyên nhân thường gặp

1. Thiết bị hoặc ứng dụng lưu mật khẩu cũ.
2. Người dùng nhập sai nhiều lần.
3. Credential Manager lưu thông tin cũ.
4. Tác vụ lập lịch hoặc dịch vụ Windows chạy bằng tài khoản người dùng.
5. Tấn công dò mật khẩu.

## Các bước xử lý

### Bước 1: Xác minh danh tính

Áp dụng cùng nguyên tắc trong bài [Quên mật khẩu](05-quen-mat-khau.md). Không mở khóa tài khoản nếu chưa xác minh được người yêu cầu.

### Bước 2: Mở khóa tài khoản

Trong Active Directory Users and Computers: tìm người dùng, mở Properties > Account, chọn **Unlock account**.

Hoặc dùng PowerShell:

```powershell
Unlock-ADAccount -Identity "ten.nguoidung"
```

### Bước 3: Tìm nguồn khóa lặp lại

Yêu cầu người dùng tắt tạm các thiết bị phụ: điện thoại, tablet, Outlook trên máy cũ, VPN. Sau đó mở khóa lại và theo dõi.

Kiểm tra Credential Manager:

Control Panel > Credential Manager > Windows Credentials, xóa thông tin cũ liên quan đến domain, file share, Outlook hoặc VPN.

### Bước 4: Kiểm tra sự kiện đăng nhập sai (Event ID 4740)

Trên Domain Controller hoặc máy quản trị, chạy PowerShell để tìm chính xác máy tính hoặc thiết bị phát sinh lần khóa tài khoản gần nhất:

```powershell
Get-WinEvent -FilterHashtable @{LogName='Security';Id=4740} -MaxEvents 5 | 
    Select-Object TimeCreated, 
        @{N='Account';E={$_.Properties[0].Value}}, 
        @{N='CallerComputer';E={$_.Properties[1].Value}}
```

Giá trị tại cột **CallerComputer** chính là tên máy tính hoặc nguồn IP đang gửi mật khẩu cũ lên hệ thống.

### Bước 5: Xử lý nguồn gây khóa

- Cập nhật mật khẩu trong Outlook, điện thoại, VPN, Wi-Fi.
- Xóa mapped drive dùng mật khẩu cũ.
- Đổi tài khoản chạy service hoặc scheduled task nếu đang dùng tài khoản cá nhân.

## Khi nào chuyển cấp (escalate)

- Tài khoản bị khóa liên tục sau khi đã xóa credential cũ.
- Event log cho thấy đăng nhập sai từ máy lạ hoặc địa chỉ lạ.
- Tài khoản có quyền cao hoặc thuộc nhóm quản trị.

**Thông tin đính kèm ticket:** thời điểm bị khóa, tần suất, thiết bị đang dùng, nguồn trong Event ID 4740 nếu có.

## Phòng ngừa

- Khuyến khích dùng SSPR và MFA.
- Không dùng tài khoản cá nhân để chạy service.
- Hướng dẫn cập nhật mật khẩu trên tất cả thiết bị sau khi đổi mật khẩu.

## Mẫu ghi chú đóng ticket

> Nguyên nhân: Outlook trên máy cũ lưu mật khẩu cũ và liên tục thử đăng nhập. Cách xử lý: xóa credential cũ, cập nhật mật khẩu mới, mở khóa tài khoản và theo dõi không còn khóa lại.

