# Không cài được phần mềm (thiếu quyền)

| | |
| --- | --- |
| Cấp độ | L1 / L2 |
| Mức ưu tiên thường gặp | P4 (Yêu cầu tiêu chuẩn); P3 nếu cần cho dự án/công việc gấp |
| Thời gian xử lý ước tính | 10-30 phút |
| Cần quyền quản trị | Có |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Windows hiện màn hình UAC yêu cầu nhập tài khoản và mật khẩu Administrator khi chạy bộ cài (`.exe`, `.msi`).
- Cài đặt báo "Access denied", "You do not have sufficient privileges" hoặc "This app has been blocked by your system administrator".
- Microsoft Store hoặc Company Portal không cài được ứng dụng.

## Câu hỏi cần hỏi người dùng trước

- Phần mềm gì, phục vụ công việc nào, có được công ty phê duyệt không?
- Người dùng tải bộ cài từ đâu?
- Máy thuộc quản lý Intune/SCCM/Group Policy không?

## Kiểm tra nhanh

- Kiểm tra xem ứng dụng đã có sẵn trên kho ứng dụng tự phục vụ của công ty (**Company Portal** hoặc **Software Center**) chưa (người dùng tự bấm cài không cần quyền admin).
- Xác định thông báo chặn là do hộp thoại UAC thông thường hay do chính sách bảo mật AppLocker / WDAC / Antivirus chặn file thực thi.
- Kiểm tra chữ ký số (Digital Signature) của file cài đặt: Chuột phải vào file `.exe` > **Properties** > **Digital Signatures** xem có chứng chỉ hợp lệ không.

## Nguyên nhân thường gặp

1. Người dùng không có quyền admin cục bộ.
2. Bộ cài không nằm trong danh sách phần mềm được phê duyệt.
3. AppLocker/Defender Application Control chặn.
4. Bộ cài hỏng hoặc không tương thích Windows.
5. Thiếu dung lượng hoặc Windows Installer lỗi.

## Các bước xử lý

### Bước 1: Xác minh nhu cầu và nguồn phần mềm

Chỉ hỗ trợ phần mềm phục vụ công việc và có nguồn chính thức. Không chạy bộ cài từ nguồn không rõ.

### Bước 2: Kiểm tra kênh cài chuẩn

Ưu tiên Company Portal, Software Center, Microsoft Store for Business hoặc share nội bộ đã phê duyệt. Nếu có gói chuẩn, hướng dẫn người dùng cài từ đó.

### Bước 3: Kiểm tra lỗi cụ thể

Ghi lại thông báo lỗi và file log nếu bộ cài tạo log. Kiểm tra dung lượng ổ C và phiên bản Windows.

### Bước 4: Cài bằng tài khoản quản trị theo quy trình

Helpdesk dùng quyền admin tạm thời hoặc công cụ quản lý phần mềm của công ty. Không chia sẻ mật khẩu admin cho người dùng.

### Bước 5: Xử lý Windows Installer

Khởi động lại máy và thử lại. Nếu dịch vụ Windows Installer lỗi:

```cmd
msiexec /unregister
msiexec /regserver
```

## Khi nào chuyển cấp (escalate)

- Phần mềm chưa được phê duyệt hoặc cần đánh giá bảo mật/license.
- AppLocker/WDAC chặn và cần tạo rule mới.
- Cần đóng gói triển khai hàng loạt.

**Thông tin đính kèm ticket:** tên phần mềm, phiên bản, nguồn tải, lý do sử dụng, ảnh lỗi, log cài đặt.

## Phòng ngừa

- Duy trì danh mục phần mềm được phê duyệt.
- Triển khai app phổ biến qua Company Portal/Software Center.
- Chuẩn hóa quy trình xin quyền cài đặt.

## Mẫu ghi chú đóng ticket

> Nguyên nhân: người dùng không có quyền admin cục bộ. Cách xử lý: xác minh phần mềm đã được phê duyệt, cài qua Company Portal, mở ứng dụng kiểm tra thành công.

