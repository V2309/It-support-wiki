# Không truy cập được ổ đĩa chia sẻ

| | |
| --- | --- |
| Cấp độ | L1 / L2 |
| Thời gian xử lý ước tính | 15-30 phút |
| Cần quyền quản trị | Có nếu cấp quyền hoặc sửa share |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Không mở được ổ mạng như `\\server\share` hoặc ổ mapped drive.
- Báo "Access denied", "Network path not found" hoặc yêu cầu nhập mật khẩu.
- Người dùng khác vào được cùng thư mục.

## Câu hỏi cần hỏi người dùng trước

- Đường dẫn share chính xác là gì?
- Người dùng đang ở văn phòng hay kết nối VPN?
- Trước đây đã truy cập được chưa, hay là yêu cầu quyền mới?

## Nguyên nhân thường gặp

1. Mất mạng hoặc chưa kết nối VPN.
2. DNS không phân giải được tên server.
3. Credential cũ lưu sai mật khẩu.
4. Người dùng thiếu quyền NTFS/share.
5. Server file share hoặc dịch vụ SMB lỗi.

## Các bước xử lý

### Bước 1: Kiểm tra kết nối mạng/VPN

Nếu ở ngoài văn phòng, kết nối VPN trước. Thử ping server:

```cmd
ping <ten-server>
```

Nếu ping bằng IP được nhưng tên server lỗi, xử lý theo [Lỗi DNS](04-loi-dns.md).

### Bước 2: Thử truy cập bằng đường dẫn UNC

Mở File Explorer và nhập:

```text
\\server\share
```

Nếu được, mapped drive cũ có thể sai. Xóa và map lại.

### Bước 3: Xóa credential cũ

Control Panel > Credential Manager > Windows Credentials, xóa credential liên quan đến file server. Đăng xuất/đăng nhập lại hoặc truy cập lại share.

### Bước 4: Map lại ổ đĩa

```cmd
net use Z: /delete
net use Z: \\server\share /persistent:yes
```

### Bước 5: Kiểm tra quyền

Nếu báo Access denied, kiểm tra người dùng thuộc nhóm quyền nào. Không tự cấp quyền nếu chưa có phê duyệt của chủ dữ liệu.

## Khi nào chuyển cấp (escalate)

- Nhiều người không vào được cùng server/share.
- Cần cấp quyền dữ liệu hoặc thay đổi nhóm AD.
- Nghi file server hết dung lượng hoặc dịch vụ SMB lỗi.

**Thông tin đính kèm ticket:** đường dẫn UNC, người dùng/nhóm, lỗi chính xác, mạng/VPN, người khác có bị không.

## Phòng ngừa

- Quản lý quyền qua nhóm AD, tránh cấp trực tiếp từng user.
- Tài liệu hóa chủ sở hữu từng share.
- Giám sát dung lượng và trạng thái file server.

## Mẫu ghi chú đóng ticket

> Nguyên nhân: Credential Manager lưu mật khẩu cũ của file server. Cách xử lý: xóa credential cũ, map lại ổ Z, người dùng truy cập thư mục thành công.

