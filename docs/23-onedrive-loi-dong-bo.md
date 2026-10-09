# OneDrive báo lỗi đồng bộ, xung đột file hoặc kẹt Processing

| | |
| --- | --- |
| Cấp độ | L1 |
| Mức ưu tiên thường gặp | P3; P2 nếu tài khoản của phòng ban bị gián đoạn tài liệu dùng chung |
| Thời gian xử lý ước tính | 15-30 phút |
| Cần quyền quản trị | Không |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Biểu tượng đám mây OneDrive dưới thanh taskbar có dấu gạch chéo đỏ, dấu chấm than hoặc xoay tròn liên tục không dừng.
- Di chuột vào biểu tượng hiện trạng thái: *"Processing changes..."* (Đang xử lý thay đổi) hoặc *"Sync pending"* hàng giờ đồng hồ.
- File trong thư mục OneDrive có biểu tượng dấu nhân đỏ (X đỏ) hoặc không cập nhật phiên bản mới nhất từ đồng nghiệp.
- Xuất hiện các file trùng tên kèm hậu tố tên máy tính (Sync Conflict - xung đột phiên bản).

## Câu hỏi cần hỏi người dùng trước

- File/thư mục bị lỗi tên là gì? Có dung lượng quá lớn (trên 15-20 GB) không?
- Kiểm tra trên web (`https://onedrive.live.com` hoặc portal M365) file đó đã có chưa?
- Tên file hoặc đường dẫn có chứa ký tự đặc biệt (`" * : < > ? / \ |`) hoặc quá dài không?
- Ổ đĩa C trên máy tính có đang bị đầy dung lượng không?

## Kiểm tra nhanh

- Bấm vào icon OneDrive ở khay hệ thống góc phải xem thông báo lỗi cụ thể.
- Kiểm tra dung lượng trống của ổ C (nếu ổ C dưới 1 GB, OneDrive sẽ tự động ngừng đồng bộ).
- Kiểm tra người dùng có đang mở đồng thời file đó trên ứng dụng khác không.

## Nguyên nhân thường gặp

1. Tên file chứa ký tự không hợp lệ hoặc tổng đường dẫn vượt quá 400 ký tự.
2. File đang bị khóa do một ứng dụng khác (Excel, Word) đang mở hoặc tiến trình ngầm chưa giải phóng.
3. Ổ đĩa cục bộ (thường là ổ C) hết dung lượng.
4. Dung lượng lưu trữ đám mây OneDrive đã vượt hạn mức (Quota full).
5. Cache cơ sở dữ liệu đồng bộ của OneDrive bị lỗi kẹt vòng lặp.

## Các bước xử lý

### Bước 1: Kiểm tra dung lượng ổ đĩa và Quota đám mây

- **Ổ đĩa cục bộ:** Mở File Explorer > This PC. Đảm bảo ổ C còn ít nhất vài GB trống. Nếu đầy, dọn dẹp tạm thời hoặc bật tính năng **Files On-Demand** (Tệp theo yêu cầu) để giải phóng dung lượng:
  - Bấm icon OneDrive > Bánh răng Cài đặt > **Settings** > Tab **Sync and backup** > **Advanced settings** > Bật **Files On-Demand** > Bấm **Free up disk space**.
- **Quota đám mây:** Xem trong Settings OneDrive xem người dùng đã dùng hết dung lượng (ví dụ 1TB/5TB) chưa.

### Bước 2: Kiểm tra tên file và đường dẫn hợp lệ

- Đảm bảo tên file và thư mục **không chứa** các ký tự: `< > : " / \ | ? *`.
- Không bắt đầu hoặc kết thúc tên file bằng dấu cách (space) hoặc dấu chấm (`.`).
- Rút ngắn đường dẫn nếu các thư mục lồng nhau quá sâu.

### Bước 3: Đóng ứng dụng đang mở file và khởi động lại OneDrive

1. Đóng toàn bộ Office (Word, Excel, PowerPoint).
2. Chuột phải vào biểu tượng OneDrive ở taskbar > Chọn biểu tượng Bánh răng > **Pause syncing** (Tạm dừng 2 giờ), sau đó bấm **Resume syncing** (Tiếp tục).
3. Nếu vẫn kẹt, bấm **Quit OneDrive** để thoát hoàn toàn, rồi vào Start gõ **OneDrive** để mở lại.

### Bước 4: Reset cấu hình và cache của OneDrive

Đây là bước hiệu quả nhất để giải quyết lỗi kẹt "Processing changes":

Mở hộp thoại Run (`Win + R`), dán lệnh sau và nhấn Enter:
```cmd
%localappdata%\Microsoft\OneDrive\onedrive.exe /reset
```

> **Lưu ý:** Lệnh này không xóa dữ liệu của người dùng, chỉ quét và xây dựng lại danh mục đồng bộ. Biểu tượng OneDrive sẽ biến mất khỏi khay hệ thống trong 1-2 phút rồi tự mở lại.

Nếu sau 2 phút icon không tự xuất hiện lại, mở Run (`Win + R`) và chạy lệnh sau để khởi động lại:
```cmd
%localappdata%\Microsoft\OneDrive\onedrive.exe
```

### Bước 5: Hủy liên kết và đăng nhập lại (Unlink this PC)

Nếu reset vẫn không giải quyết được:
1. Bấm icon OneDrive > Cài đặt (Bánh răng) > **Settings**.
2. Chọn mục **Account** > Bấm **Unlink this PC** (Hủy liên kết PC này) > Xác nhận.
3. Đăng nhập lại bằng email công ty của người dùng, chọn giữ nguyên vị trí thư mục OneDrive cũ để không phải tải lại toàn bộ file.

## Khi nào chuyển cấp (escalate)

- Mailbox hoặc tài khoản M365 bị khóa quyền OneDrive/SharePoint từ trung tâm quản trị.
- Nghi ngờ mất dữ liệu file quan trọng hoặc file bị ghi đè không thể khôi phục qua lịch sử phiên bản (Version History).
- Lỗi đồng bộ diện rộng trên các thư mục SharePoint dùng chung của phòng ban.

**Thông tin đính kèm ticket:** Tên tài khoản, tên file/thư mục lỗi, ảnh chụp lỗi OneDrive, dung lượng ổ C, mã lỗi hiển thị (nếu có).

## Phòng ngừa

- Hướng dẫn người dùng luôn bật tính năng **Files On-Demand** để tránh tràn ổ C.
- Khuyên người dùng tận dụng tính năng **Version History** (Lịch sử phiên bản) trên web khi gặp xung đột file.
- Không đặt tên file quá dài hoặc chứa ký tự đặc biệt.

## Mẫu ghi chú đóng ticket

> Nguyên nhân: OneDrive bị kẹt trạng thái Processing changes do xung đột file cache sau khi mạng chập chờn. Cách xử lý: chạy lệnh onedrive.exe /reset, OneDrive đã quét lại danh mục và đồng bộ toàn bộ file lên đám mây thành công. Đã kiểm tra icon đám mây báo "Up to date".
