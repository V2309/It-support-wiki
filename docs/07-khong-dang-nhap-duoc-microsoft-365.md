# Không đăng nhập được Microsoft 365

| | |
| --- | --- |
| Cấp độ | L1 / L2 |
| Mức ưu tiên thường gặp | P3; P1/P2 nếu dịch vụ Microsoft 365 gián đoạn diện rộng |
| Thời gian xử lý ước tính | 10-30 phút |
| Cần quyền quản trị | Có nếu kiểm tra license, MFA hoặc trạng thái tài khoản |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Không đăng nhập được Outlook, Teams, OneDrive hoặc portal.office.com.
- Báo sai mật khẩu, cần MFA, tài khoản bị khóa hoặc không có license.
- Vòng lặp đăng nhập liên tục trong trình duyệt hoặc ứng dụng Office.

## Câu hỏi cần hỏi người dùng trước

- Lỗi xảy ra trên web, app desktop hay cả hai?
- Có đổi mật khẩu, đổi điện thoại MFA hoặc đi công tác nước ngoài không?
- Người dùng khác có đăng nhập được không?

## Kiểm tra nhanh

- Thử đăng nhập trên trình duyệt bằng chế độ ẩn danh (InPrivate/Incognito) để loại trừ cache/cookie cũ.
- Kiểm tra trạng thái tài khoản trên Microsoft Entra admin center (`Block sign-in`, `Account status`).
- Kiểm tra trang **Service Health** trong Microsoft 365 admin center xem Microsoft có đang bị sự cố toàn cầu không.

## Nguyên nhân thường gặp

1. Sai mật khẩu hoặc tài khoản bị khóa.
2. MFA không hoàn tất.
3. License Microsoft 365 bị gỡ hoặc hết hạn.
4. Trình duyệt lưu cookie/token lỗi.
5. Conditional Access chặn vị trí, thiết bị hoặc rủi ro đăng nhập.

## Các bước xử lý

### Bước 1: Thử đăng nhập trên web

Mở cửa sổ InPrivate/Incognito và truy cập:

```text
https://portal.office.com
```

Nếu đăng nhập được trên web nhưng app desktop lỗi, chuyển sang bước 4.

### Bước 2: Kiểm tra tài khoản

- Xác minh mật khẩu đúng bằng một dịch vụ khác.
- Nếu bị khóa hoặc quên mật khẩu, xử lý theo [Quên mật khẩu](05-quen-mat-khau.md) hoặc [Tài khoản bị khóa](06-tai-khoan-bi-khoa-active-directory.md).
- Trong Microsoft 365 admin center, kiểm tra tài khoản có bị block sign-in không.

### Bước 3: Kiểm tra license

Microsoft 365 admin center > Users > Active users > chọn người dùng > Licenses and apps. Đảm bảo có license phù hợp cho Exchange, Teams, OneDrive.

### Bước 4: Xóa phiên đăng nhập lỗi trên máy

- Đăng xuất khỏi Office.
- Settings > Accounts > Access work or school: ngắt kết nối tài khoản công ty nếu được phép, rồi kết nối lại.
- Control Panel > Credential Manager: xóa credential liên quan `MicrosoftOffice`, `ADAL`, `OneDrive`.
- Mở lại ứng dụng và đăng nhập.

### Bước 5: Kiểm tra MFA và Conditional Access

Nếu lỗi liên quan MFA, xử lý theo [Đổi điện thoại, không nhận mã MFA](08-doi-dien-thoai-khong-nhan-ma-mfa.md). Nếu bị chặn bởi chính sách vị trí hoặc thiết bị, chuyển nhóm Entra ID/Security.

## Khi nào chuyển cấp (escalate)

- Lỗi Conditional Access, risky sign-in hoặc cần điều tra bảo mật.
- License không cấp được do hết số lượng.
- Nhiều người cùng không đăng nhập được Microsoft 365.

**Thông tin đính kèm ticket:** ảnh lỗi, app bị ảnh hưởng, đăng nhập web có được không, thời điểm lỗi, trạng thái license.

## Phòng ngừa

- Theo dõi license còn trống.
- Hướng dẫn người dùng đăng ký nhiều phương thức MFA.
- Chuẩn hóa quy trình offboarding để không gỡ nhầm license.

## Mẫu ghi chú đóng ticket

> Nguyên nhân: credential Office cũ trên máy gây vòng lặp đăng nhập. Cách xử lý: xóa credential MicrosoftOffice/ADAL, đăng nhập lại Outlook và Teams thành công.

