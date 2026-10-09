# Đổi điện thoại, không nhận mã xác thực MFA

| | |
| --- | --- |
| Cấp độ | L1 / L2 |
| Mức ưu tiên thường gặp | P3; P2 nếu ảnh hưởng tài khoản quản lý/VIP cần truy cập khẩn |
| Thời gian xử lý ước tính | 10-25 phút |
| Cần quyền quản trị | Có nếu reset phương thức MFA |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Người dùng đổi điện thoại và không nhận được mã hoặc thông báo từ Microsoft Authenticator.
- Số điện thoại cũ không còn dùng được.
- Không thể hoàn tất đăng nhập vì bị kẹt ở bước MFA.

## Câu hỏi cần hỏi người dùng trước

- Còn giữ điện thoại cũ không?
- Có đăng ký phương thức dự phòng như SMS, cuộc gọi, mã khôi phục không?
- Yêu cầu đến từ người dùng thật hay do người khác nhờ hộ?

## Kiểm tra nhanh

- Kiểm tra xem người dùng có bấm vào "Sign in another way" trên màn hình đăng nhập để dùng phương thức khác (SMS/email dự phòng) chưa.
- Kiểm tra điện thoại mới đã bật kết nối mạng (Wi-Fi/4G) và cho phép thông báo (Notifications) cho app Microsoft Authenticator chưa.
- Kiểm tra cài đặt ngày giờ trên điện thoại mới có bật chế độ "Tự động cập nhật giờ" (Set Automatically) không.

## Nguyên nhân thường gặp

1. Authenticator chưa được chuyển sang điện thoại mới.
2. Số điện thoại MFA cũ đã mất.
3. Đồng hồ điện thoại lệch giờ.
4. Người dùng chưa đăng ký phương thức dự phòng.

## Các bước xử lý

### Bước 1: Xác minh danh tính nghiêm ngặt

MFA là lớp bảo vệ tài khoản. Chỉ reset sau khi xác minh theo quy trình công ty: gọi lại số đã đăng ký, kiểm tra thẻ nhân viên, xác nhận quản lý hoặc gặp trực tiếp.

### Bước 2: Nếu còn phương thức dự phòng

Hướng dẫn người dùng vào:

```text
https://mysignins.microsoft.com/security-info
```

Thêm điện thoại mới, đặt làm phương thức mặc định, sau đó xóa thiết bị cũ.

### Bước 3: Nếu không còn phương thức nào

Quản trị viên vào Entra admin center > Users > chọn người dùng > Authentication methods:

- Xóa phương thức cũ không còn dùng.
- Yêu cầu đăng ký lại MFA.
- Có thể cấp Temporary Access Pass nếu công ty cho phép.

### Bước 4: Kiểm tra điện thoại mới

- Đồng bộ thời gian tự động.
- Cài Microsoft Authenticator bản mới nhất.
- Bật thông báo push.
- Thử đăng nhập lại và xác nhận người dùng nhận được prompt.

## Khi nào chuyển cấp (escalate)

- Không xác minh được danh tính.
- Tài khoản đặc quyền hoặc có dấu hiệu bị chiếm quyền.
- Cần thay đổi chính sách MFA hoặc Temporary Access Pass.

**Thông tin đính kèm ticket:** cách xác minh, phương thức đã reset, thời điểm, người phê duyệt nếu có.

## Phòng ngừa

- Yêu cầu người dùng đăng ký ít nhất hai phương thức MFA.
- Nhắc cập nhật MFA trước khi đổi hoặc trả điện thoại.
- Có quy trình cấp Temporary Access Pass được phê duyệt.

## Mẫu ghi chú đóng ticket

> Nguyên nhân: người dùng đổi điện thoại và mất Authenticator cũ. Cách xử lý: xác minh danh tính qua số đã đăng ký và quản lý xác nhận, reset phương thức MFA, người dùng đăng ký lại Authenticator thành công.

