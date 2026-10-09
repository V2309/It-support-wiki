# Wi-Fi kết nối nhưng không có Internet

| | |
| --- | --- |
| Cấp độ | L1 |
| Thời gian xử lý ước tính | 10-20 phút |
| Cần quyền quản trị | Không, trừ khi cài lại driver |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Máy đã kết nối Wi-Fi nhưng trình duyệt báo không có Internet.
- Biểu tượng Wi-Fi có dấu chấm than hoặc thông báo "No Internet, secured".
- Các thiết bị khác cùng Wi-Fi vẫn dùng được hoặc chỉ một khu vực bị ảnh hưởng.

## Câu hỏi cần hỏi người dùng trước

- Wi-Fi nào đang kết nối? Có đúng SSID công ty không?
- Thiết bị khác của người dùng có vào Internet được không?
- Lỗi bắt đầu sau khi đổi mật khẩu Wi-Fi, đổi vị trí ngồi hoặc cập nhật Windows không?

## Nguyên nhân thường gặp

1. Nhập sai mật khẩu hoặc máy lưu cấu hình Wi-Fi cũ.
2. Máy không nhận IP từ DHCP.
3. Tín hiệu yếu hoặc roaming giữa các access point lỗi.
4. Captive portal của Wi-Fi khách chưa được chấp nhận.
5. DNS hoặc proxy sai.

## Các bước xử lý

### Bước 1: Quên mạng Wi-Fi và kết nối lại

Settings > Network & Internet > Wi-Fi > Manage known networks, chọn SSID, bấm **Forget**, sau đó kết nối lại bằng mật khẩu đúng.

**Kết quả mong đợi:** máy kết nối lại và có Internet. Nếu vẫn lỗi, sang bước 2.

### Bước 2: Kiểm tra IP

Mở Command Prompt:

```cmd
ipconfig /all
```

Nếu IP là `169.254.x.x`, chạy:

```cmd
ipconfig /release
ipconfig /renew
```

Nếu vẫn không nhận IP, thử Wi-Fi khác hoặc chuyển vị trí gần access point hơn.

### Bước 3: Kiểm tra DNS và gateway

```cmd
ping <gateway>
ping 8.8.8.8
ping microsoft.com
```

Ping được IP nhưng không ping được tên miền là lỗi DNS, xử lý theo bài [Lỗi DNS](04-loi-dns.md).

### Bước 4: Kiểm tra proxy và captive portal

- Settings > Network & Internet > Proxy: tắt proxy nếu công ty không dùng.
- Với Wi-Fi khách, mở trình duyệt vào `http://neverssl.com` để hiện trang chấp nhận điều khoản.

### Bước 5: Cập nhật hoặc cài lại driver Wi-Fi

Device Manager > Network adapters, kiểm tra card Wi-Fi có dấu chấm than không. Nếu có, cập nhật driver từ nhà sản xuất hoặc gỡ thiết bị rồi quét lại phần cứng.

## Khi nào chuyển cấp (escalate)

- Nhiều người cùng khu vực mất Internet qua Wi-Fi.
- Chỉ một SSID lỗi, SSID khác bình thường.
- Máy không nhận IP dù đã thử nhiều access point.

**Thông tin đính kèm ticket:** SSID, vị trí, kết quả `ipconfig /all`, thiết bị khác có bị không, ảnh lỗi.

## Phòng ngừa

- Tách Wi-Fi nội bộ và Wi-Fi khách rõ ràng.
- Lưu tài liệu SSID chuẩn, vùng phủ sóng và chính sách proxy.
- Cập nhật driver Wi-Fi qua công cụ quản lý thiết bị.

## Mẫu ghi chú đóng ticket

> Nguyên nhân: máy lưu cấu hình Wi-Fi cũ sau khi đổi mật khẩu. Cách xử lý: quên SSID, kết nối lại, máy nhận IP hợp lệ và truy cập Internet bình thường.

