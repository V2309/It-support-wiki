# Vào được IP nhưng không vào được tên miền (lỗi DNS)

| | |
| --- | --- |
| Cấp độ | L1 / L2 |
| Mức ưu tiên thường gặp | P3; P2 nếu toàn bộ phòng ban không phân giải được tên miền nội bộ |
| Thời gian xử lý ước tính | 10-25 phút |
| Cần quyền quản trị | Có nếu đổi cấu hình card mạng |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Ping `8.8.8.8` được nhưng ping `google.com` thất bại.
- Trình duyệt báo `DNS_PROBE_FINISHED_NXDOMAIN` hoặc `DNS server not responding`.
- Không truy cập được tài nguyên nội bộ bằng tên máy chủ, nhưng vào bằng IP được.

## Câu hỏi cần hỏi người dùng trước

- Lỗi xảy ra với mọi website hay chỉ website nội bộ?
- Người dùng đang ở mạng công ty, Wi-Fi khách hay VPN?
- Có vừa đổi DNS, proxy, VPN hoặc phần mềm bảo mật không?

## Kiểm tra nhanh

- Chạy `ipconfig /displaydns` hoặc `nslookup` xem DNS Server IP hiện tại của máy là IP nội bộ (Domain Controller) hay IP công cộng (8.8.8.8 / 1.1.1.1).
- So sánh kết quả `nslookup` trên máy bị lỗi với một máy trạm hoạt động bình thường bên cạnh.
- Kiểm tra file `hosts` tại `C:\Windows\System32\drivers\etc\hosts` xem có bản ghi tĩnh nào bị ghi đè không.

## Nguyên nhân thường gặp

1. DNS server không phản hồi.
2. Máy đang dùng DNS công cộng thay vì DNS nội bộ.
3. Cache DNS lỗi.
4. VPN không đẩy DNS nội bộ xuống máy trạm.
5. Bản ghi DNS nội bộ bị thiếu hoặc sai.

## Các bước xử lý

### Bước 1: Xác nhận lỗi DNS

```cmd
ping 8.8.8.8
nslookup google.com
nslookup <ten-may-chu-noi-bo>
```

Nếu ping IP được nhưng `nslookup` lỗi, tiếp tục bước 2.

### Bước 2: Xóa cache DNS

```cmd
ipconfig /flushdns
ipconfig /registerdns
```

Thử lại `nslookup`. Nếu vẫn lỗi, kiểm tra DNS đang dùng.

### Bước 3: Kiểm tra DNS trên card mạng

```cmd
ipconfig /all
```

So sánh mục **DNS Servers** với DNS chuẩn của công ty. Máy trong domain thường cần dùng DNS nội bộ, không nên tự đổi sang DNS công cộng nếu cần truy cập tài nguyên domain.

### Bước 4: Kiểm tra DNS khi dùng VPN

Kết nối VPN, chạy lại `ipconfig /all` và kiểm tra adapter VPN có DNS nội bộ không. Nếu VPN không cấp DNS hoặc split DNS sai, chuyển L2/network.

### Bước 5: Kiểm tra file hosts

Mở Notepad bằng quyền quản trị và kiểm tra:

```text
C:\Windows\System32\drivers\etc\hosts
```

Xóa dòng trỏ sai nếu có phê duyệt và ghi lại thay đổi vào ticket.

## Khi nào chuyển cấp (escalate)

- Nhiều người cùng không phân giải được tên miền.
- DNS nội bộ không phản hồi hoặc bản ghi DNS bị thiếu.
- Lỗi chỉ xảy ra khi kết nối VPN và cần sửa cấu hình server VPN.

**Thông tin đính kèm ticket:** kết quả `ipconfig /all`, `nslookup`, mạng đang dùng, tên miền bị lỗi.

## Phòng ngừa

- Duy trì danh sách DNS chuẩn theo site.
- Không hướng dẫn người dùng tự đổi DNS nếu máy nằm trong domain.
- Giám sát DNS server và sao lưu vùng DNS nội bộ.

## Mẫu ghi chú đóng ticket

> Nguyên nhân: máy đang dùng DNS công cộng nên không phân giải được tên máy chủ nội bộ. Cách xử lý: đổi về DNS nội bộ theo chuẩn site, xóa cache DNS, truy cập lại ổ chia sẻ thành công.

