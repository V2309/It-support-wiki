# Không vào được mạng

| | |
| --- | --- |
| Cấp độ | L1 |
| Mức ưu tiên thường gặp | P3; P1/P2 nếu nhiều người hoặc cả khu vực bị ảnh hưởng |
| Thời gian xử lý ước tính | 10-20 phút |
| Cần quyền quản trị | Một số bước cuối (reset Winsock) |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Biểu tượng mạng có dấu chấm than vàng hoặc dấu X đỏ.
- Trình duyệt báo "No internet", "DNS_PROBE_FINISHED_NO_INTERNET" hoặc "This site can't be reached".
- Không truy cập được ứng dụng nội bộ hoặc ổ đĩa chia sẻ.

## Câu hỏi cần hỏi người dùng trước

- Dùng cáp mạng hay Wi-Fi?
- Chỉ máy này bị hay đồng nghiệp xung quanh cũng bị?
- Hôm qua còn dùng được không? Có đổi chỗ ngồi, đổi mật khẩu Wi-Fi hoặc cài phần mềm mới không?
- Có truy cập được trang nội bộ nhưng không ra Internet, hay hoàn toàn không có gì?

Nếu nhiều người cùng bị, đừng xử lý từng máy: chuyển ngay cho nhóm mạng (xem mục "Khi nào chuyển cấp").

## Kiểm tra nhanh

- Xác định chỉ một máy hay nhiều máy cùng mất mạng.
- Kiểm tra cáp/Wi-Fi, chế độ máy bay và biểu tượng mạng.
- Chạy `ipconfig /all` và ghi lại IP, gateway, DNS.

## Nguyên nhân thường gặp

1. Cáp mạng lỏng, hỏng hoặc cổng switch tắt.
2. Wi-Fi bị tắt (phím tắt, chế độ máy bay) hoặc nhập sai mật khẩu.
3. Máy không nhận được địa chỉ IP từ DHCP (địa chỉ dạng `169.254.x.x`).
4. Cấu hình IP, DNS hoặc proxy sai.
5. Sự cố ở switch, router hoặc nhà cung cấp Internet.

## Các bước xử lý

### Bước 1: Kiểm tra vật lý và công tắc

- Cáp mạng: cắm lại hai đầu, thử cổng khác hoặc cáp khác. Đèn ở cổng mạng phải sáng.
- Wi-Fi: kiểm tra chế độ máy bay và phím tắt Wi-Fi trên laptop, thử bật tắt lại.
- Thử khởi động lại máy nếu chưa làm.

### Bước 2: Xem địa chỉ IP của máy

Mở Command Prompt (không cần quyền quản trị) và chạy:

```cmd
ipconfig /all
```

Xem các giá trị của card mạng đang dùng:

| Kết quả | Ý nghĩa |
| --- | --- |
| IP dạng `169.254.x.x` | Máy không nhận được IP từ DHCP: làm Bước 3 |
| IP hợp lệ (ví dụ `192.168.1.25`) | Có IP, chuyển sang Bước 4 |
| "Media disconnected" | Cáp hoặc Wi-Fi chưa kết nối: quay lại Bước 1 |

### Bước 3: Xin lại địa chỉ IP

```cmd
ipconfig /release
ipconfig /renew
```

**Kết quả mong đợi:** máy nhận IP hợp lệ. Nếu vẫn là `169.254.x.x`, thử cổng mạng khác hoặc máy khác để xác định lỗi ở máy hay ở hệ thống (DHCP, switch). Nếu máy khác cùng cổng vẫn lỗi, chuyển cấp.

### Bước 4: Ping theo từng lớp để xác định điểm đứt

Thực hiện theo thứ tự, dừng ở lệnh đầu tiên thất bại:

```cmd
ping 127.0.0.1
ping <địa chỉ gateway trong ipconfig /all>
ping 8.8.8.8
ping google.com
```

| Lệnh thất bại | Khả năng nguyên nhân |
| --- | --- |
| `127.0.0.1` | Lỗi ngăn xếp TCP/IP hoặc driver card mạng: làm Bước 6 |
| Gateway | Lỗi cáp, Wi-Fi, switch hoặc cấu hình IP |
| `8.8.8.8` | Router hoặc đường truyền Internet có sự cố: chuyển cấp |
| `google.com` (nhưng `8.8.8.8` được) | Lỗi DNS: làm Bước 5 |

Lưu ý: một số mạng chặn ping (ICMP). Nếu ping thất bại nhưng người dùng vẫn mở được web thì không phải lỗi mạng.

### Bước 5: Xóa bộ nhớ đệm DNS và kiểm tra DNS

```cmd
ipconfig /flushdns
nslookup google.com
```

Nếu `nslookup` báo lỗi, kiểm tra máy đang dùng DNS nào trong `ipconfig /all` và so với DNS chuẩn của công ty. Không tự đổi sang DNS công cộng khi máy cần truy cập tài nguyên nội bộ.

### Bước 6: Đặt lại cấu hình mạng của Windows (cần quyền quản trị)

Chỉ chạy bước này sau khi đã ghi lại cấu hình IP tĩnh, DNS, proxy hoặc VPN nếu máy đang dùng cấu hình đặc biệt.

Mở Command Prompt bằng "Run as administrator":

```cmd
netsh winsock reset
netsh int ip reset
```

**Khởi động lại máy** sau khi chạy. Hai lệnh này xóa cấu hình mạng tùy chỉnh (ví dụ IP tĩnh), nên ghi lại cấu hình hiện tại trước khi chạy.

### Bước 7: Kiểm tra driver và proxy

- Device Manager > Network adapters: nếu card mạng có dấu chấm than, gỡ driver và quét lại thiết bị, hoặc cài driver từ nhà sản xuất.
- Settings > Network & Internet > Proxy: tắt proxy nếu công ty không yêu cầu.

## Khi nào chuyển cấp (escalate)

- Nhiều người hoặc cả khu vực cùng mất mạng.
- Ping gateway được nhưng không ra Internet, và máy khác cùng mạng cũng bị.
- Máy không nhận IP ở bất kỳ cổng nào.
- Nghi ngờ cổng switch hỏng hoặc cáp âm tường.

**Thông tin đính kèm ticket:** tên máy, vị trí, kết quả `ipconfig /all`, lệnh ping nào thất bại, thời điểm bắt đầu lỗi, bao nhiêu người bị ảnh hưởng.

## Phòng ngừa

- Dán nhãn cổng mạng và cáp để dễ kiểm tra.
- Giữ tài liệu chuẩn về dải IP, DNS và gateway của từng khu vực.
- Ghi lại cấu hình IP tĩnh của các máy đặc biệt trước khi thay đổi.

## Mẫu ghi chú đóng ticket

> Nguyên nhân: máy không nhận IP từ DHCP do cáp mạng lỏng. Cách xử lý: cắm lại cáp, chạy `ipconfig /renew`, máy nhận IP 192.168.1.25 và truy cập Internet bình thường. Đã xác nhận với người dùng.
