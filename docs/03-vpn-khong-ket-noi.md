# VPN không kết nối

| | |
| --- | --- |
| Cấp độ | L1 / L2 |
| Mức ưu tiên thường gặp | P3; P1/P2 nếu hệ thống VPN toàn công ty hoặc nhiều người làm việc từ xa cùng bị |
| Thời gian xử lý ước tính | 15-30 phút |
| Cần quyền quản trị | Một số bước (cài lại client, đổi cấu hình) |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Ứng dụng VPN báo "Connection failed", "Timeout", "Authentication failed" hoặc kẹt ở trạng thái "Connecting".
- VPN nối được nhưng không truy cập được tài nguyên nội bộ.
- VPN hay tự ngắt kết nối.

Cách xử lý phụ thuộc phần mềm VPN công ty dùng (GlobalProtect, FortiClient, Cisco AnyConnect, OpenVPN, VPN tích hợp Windows...). Bài này nêu các bước chung; hãy tham khảo tài liệu riêng của công ty cho giao diện cụ thể.

## Câu hỏi cần hỏi người dùng trước

- Người dùng đang ở đâu (nhà, quán cà phê, khách sạn, 4G)?
- Có truy cập Internet bình thường không?
- Thông báo lỗi chính xác là gì? (nhờ chụp màn hình)
- VPN dùng được lần cuối khi nào? Có đổi mật khẩu, đổi máy, cập nhật Windows gần đây không?
- Những người khác có kết nối được không?

## Kiểm tra nhanh

- Thử phát Wi-Fi từ 4G điện thoại để loại trừ mạng Wi-Fi tại nhà/khách sạn chặn cổng VPN (IPSec, SSL, UDP 4500).
- Kiểm tra đồng hồ hệ thống trên Windows xem có bị lệch giờ so với thực tế không.
- Kiểm tra tài khoản người dùng có đang bị khóa (Lockout) hoặc hết hạn mật khẩu trên AD không.

## Nguyên nhân thường gặp

1. Máy người dùng không có Internet ổn định.
2. Sai mật khẩu, tài khoản bị khóa hoặc mật khẩu hết hạn.
3. Mã xác thực MFA sai hoặc thiết bị MFA bị đổi.
4. Giờ hệ thống của máy bị lệch (gây lỗi chứng chỉ, mã MFA).
5. Mạng đang dùng chặn cổng VPN (mạng khách sạn, quán cà phê, một số nhà mạng).
6. Phần mềm VPN lỗi thời hoặc hỏng.
7. Phần mềm diệt virus hoặc tường lửa chặn VPN.
8. Máy chủ VPN quá tải hoặc đang bảo trì.

## Các bước xử lý

### Bước 1: Xác nhận Internet hoạt động

Mở một trang web bất kỳ (ví dụ `https://www.microsoft.com`). Nếu không vào được, xử lý theo bài [Không vào được mạng](01-khong-vao-duoc-mang.md) trước.

### Bước 2: Kiểm tra tài khoản và MFA

- Thử đăng nhập vào một dịch vụ khác dùng cùng tài khoản (ví dụ Microsoft 365) để xác nhận mật khẩu còn đúng.
- Nếu tài khoản bị khóa hoặc hết hạn mật khẩu: xử lý theo bài [Quên mật khẩu](05-quen-mat-khau.md).
- Kiểm tra mã MFA: đồng hồ trên điện thoại phải đúng giờ; thử gửi lại mã.

### Bước 3: Kiểm tra giờ hệ thống

Settings > Time & language > Date & time: bật **Set time automatically** và **Set time zone automatically**, bấm **Sync now**.

### Bước 4: Thử mạng khác

Chuyển sang điểm phát sóng 4G/5G trên điện thoại rồi thử kết nối VPN.

- Kết nối được qua 4G: mạng ban đầu đang chặn VPN. Giải pháp là dùng mạng khác hoặc nhờ quản trị mạng hướng dẫn đổi giao thức/cổng (ví dụ dùng SSL VPN cổng 443 thay vì IPsec).
- Vẫn không kết nối được: lỗi nằm ở máy hoặc ở máy chủ VPN.

### Bước 5: Khởi động lại và cập nhật client

1. Thoát hoàn toàn ứng dụng VPN (kiểm tra khay hệ thống), mở lại.
2. Khởi động lại máy.
3. Kiểm tra phiên bản client với bản chuẩn của công ty và cập nhật nếu cũ.

### Bước 6: Xóa cache DNS và làm mới mạng

```cmd
ipconfig /flushdns
ipconfig /release
ipconfig /renew
```

### Bước 7: Kiểm tra phần mềm bảo mật

Tạm thời kiểm tra xem tường lửa hoặc phần mềm diệt virus có chặn VPN không (xem nhật ký chặn, không tắt hẳn bảo vệ nếu chưa được phép). Nếu xác định được, nhờ nhóm bảo mật thêm ngoại lệ.

### Bước 8: Cài lại client VPN (cần quyền quản trị)

1. Gỡ ứng dụng VPN và các adapter ảo của nó (Device Manager > Network adapters).
2. Khởi động lại máy.
3. Cài bản chuẩn của công ty và nhập lại cấu hình.

### Bước 9: VPN nối được nhưng không vào được tài nguyên nội bộ

- Kiểm tra IP VPN đã cấp: `ipconfig /all` sẽ có thêm một adapter VPN.
- Thử `ping` máy chủ nội bộ bằng IP, rồi bằng tên. Ping được IP nhưng không được tên: lỗi DNS khi dùng VPN (kiểm tra cấu hình DNS của VPN hoặc split tunneling).
- Tài khoản có thể thiếu quyền truy cập tài nguyên đó: chuyển cấp để kiểm tra nhóm quyền.

## Lỗi thường gặp trên VPN tích hợp của Windows

| Mã lỗi | Ý nghĩa thường gặp | Hướng xử lý |
| --- | --- | --- |
| 691 | Sai tên đăng nhập hoặc mật khẩu | Kiểm tra tài khoản, xem tài khoản có bị khóa không |
| 800 | Không tạo được kết nối tới máy chủ | Kiểm tra Internet, địa chỉ máy chủ VPN, tường lửa hoặc mạng đang chặn VPN |
| 809 | Không thiết lập được kết nối (thường do tường lửa hoặc NAT chặn L2TP/IPsec) | Thử mạng khác; cấu hình registry cần quyền quản trị, chuyển cho L2 |

## Khi nào chuyển cấp (escalate)

- Nhiều người cùng không kết nối được VPN (nghi máy chủ hoặc đường truyền).
- Lỗi chứng chỉ, cấu hình phía máy chủ hoặc cần thay đổi quy tắc tường lửa.
- Cần cấp thêm quyền truy cập tài nguyên cho người dùng.
- Nghi ngờ bị tấn công (nhiều lần đăng nhập thất bại từ địa chỉ lạ).

**Thông tin đính kèm ticket:** tên người dùng, vị trí và loại mạng đang dùng, tên và phiên bản client VPN, thông báo lỗi (ảnh chụp màn hình), thời điểm lỗi, các bước đã thử.

## Phòng ngừa

- Gửi hướng dẫn cài và dùng VPN cho nhân viên mới, kèm ảnh chụp màn hình.
- Chuẩn hóa phiên bản client và tự động cập nhật.
- Có sẵn phương án dự phòng (cổng 443) cho nhân viên hay đi công tác.
- Theo dõi tải máy chủ VPN vào giờ cao điểm.

## Mẫu ghi chú đóng ticket

> Nguyên nhân: mạng khách sạn chặn cổng VPN. Cách xử lý: chuyển sang điểm phát sóng 4G, kết nối VPN thành công và truy cập được ổ đĩa chia sẻ. Đã hướng dẫn người dùng dùng 4G khi đi công tác. Đã xác nhận với người dùng.
