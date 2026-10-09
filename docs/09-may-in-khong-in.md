# Máy in không in

| | |
| --- | --- |
| Cấp độ | L1 |
| Mức ưu tiên thường gặp | P3; P2 nếu nhiều người cùng không in được |
| Thời gian xử lý ước tính | 10-20 phút |
| Cần quyền quản trị | Có (khởi động lại Print Spooler, cài driver) |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Lệnh in được gửi đi nhưng giấy không ra.
- Trạng thái máy in là "Offline", "Error" hoặc "Printing" mãi không kết thúc.
- Hàng đợi in có tài liệu bị kẹt, không xóa được.
- Máy in biến mất khỏi danh sách hoặc không thêm được máy in.

## Câu hỏi cần hỏi người dùng trước

- Máy in có đang bật không? Màn hình máy in báo gì (hết giấy, kẹt giấy, hết mực)?
- Những người khác in được không?
- In được từ tất cả ứng dụng hay chỉ một ứng dụng?
- Máy in nối bằng USB, mạng nội bộ hay qua print server?

## Kiểm tra nhanh

- Kiểm tra màn hình máy in có báo hết giấy, kẹt giấy, hết mực hoặc lỗi phần cứng không.
- Xác định chỉ một người hay nhiều người cùng không in được.
- In thử từ Notepad hoặc in test page để loại trừ lỗi ứng dụng.

## Nguyên nhân thường gặp

1. Máy in tắt, hết giấy, kẹt giấy, hết mực hoặc có lỗi phần cứng.
2. Hàng đợi in bị kẹt (dịch vụ Print Spooler treo).
3. Chọn nhầm máy in mặc định.
4. Máy in mất kết nối mạng hoặc đổi địa chỉ IP.
5. Driver lỗi hoặc không tương thích sau khi cập nhật Windows.

## Các bước xử lý

### Bước 1: Kiểm tra máy in

- Nguồn điện, cáp mạng/USB, màn hình hiển thị lỗi.
- Giấy, mực, nắp đậy, khay giấy.
- In thử một trang từ chính máy in (thường qua menu hoặc giữ nút). Nếu không in được, đây là lỗi phần cứng: chuyển cấp hoặc gọi đơn vị bảo trì.

### Bước 2: Kiểm tra máy in mặc định và trạng thái

Settings > Bluetooth & devices > Printers & scanners:

- Chọn đúng máy in cần dùng.
- Bỏ tích "Use offline" nếu có (trên cửa sổ hàng đợi in: Printer > bỏ chọn **Use Printer Offline**).
- Tắt "Let Windows manage my default printer" nếu máy hay đổi máy in mặc định.

### Bước 3: Kiểm tra kết nối mạng đến máy in

Với máy in mạng, mở Command Prompt:

```cmd
ping <địa chỉ IP của máy in>
```

- Ping thành công: máy in trên mạng, lỗi nằm ở máy tính hoặc driver.
- Ping thất bại: kiểm tra cáp, Wi-Fi của máy in, hoặc IP đã bị đổi (in trang cấu hình mạng từ máy in để xem IP hiện tại).

Nếu IP máy in đã đổi, cập nhật lại cổng in (Printer properties > Ports > Configure Port) hoặc nhờ nhóm mạng đặt IP tĩnh/DHCP reservation cho máy in.

### Bước 4: Xóa hàng đợi in bị kẹt (cần quyền quản trị)

Thông báo trước cho người dùng vì thao tác này sẽ xóa các lệnh in đang chờ trên máy hiện tại.

Mở Command Prompt bằng "Run as administrator":

```cmd
net stop spooler
del /Q /F /S "%systemroot%\System32\spool\PRINTERS\*.*"
net start spooler
```

**Kết quả mong đợi:** hàng đợi trống, in thử lại thành công.

Cảnh báo: lệnh `del` xóa mọi lệnh in đang chờ của máy này. Báo trước cho người dùng nếu họ có tài liệu quan trọng đang chờ in.

Cách tương đương bằng PowerShell:

```powershell
Restart-Service -Name Spooler -Force
Get-PrintJob -PrinterName "Tên máy in" | Remove-PrintJob
```

### Bước 5: Cài lại máy in và driver

1. Gỡ máy in khỏi danh sách (Printers & scanners > Remove).
2. Nếu nghi driver lỗi: Print Management hoặc Print Server Properties > Drivers > gỡ driver cũ.
3. Cài driver mới nhất từ trang của nhà sản xuất, đúng model và đúng phiên bản Windows 64-bit.
4. Thêm lại máy in (theo IP hoặc qua print server của công ty).
5. In thử trang kiểm tra (Printer properties > Print Test Page).

### Bước 6: Kiểm tra theo ứng dụng

Nếu chỉ một ứng dụng không in được: thử in từ Notepad, nếu thành công thì lỗi nằm ở cài đặt hoặc bản cài của ứng dụng đó (thử in ra PDF, cập nhật hoặc sửa chữa ứng dụng).

## Khi nào chuyển cấp (escalate)

- Nhiều người cùng không in được trên một máy in hoặc qua một print server.
- Máy in báo lỗi phần cứng (đèn đỏ, mã lỗi).
- Dịch vụ Print Spooler liên tục dừng sau khi khởi động lại.
- Cần đổi IP, cấu hình print server hoặc chính sách triển khai máy in qua Group Policy.

**Thông tin đính kèm ticket:** tên và model máy in, IP, ai bị ảnh hưởng, thông báo lỗi trên máy in và trên máy tính, các bước đã thử.

## Phòng ngừa

- Đặt IP tĩnh hoặc DHCP reservation cho máy in.
- Chuẩn hóa driver và triển khai máy in qua print server hoặc Group Policy.
- Thay vật tư (mực, trống) định kỳ, theo dõi cảnh báo từ máy in.

## Mẫu ghi chú đóng ticket

> Nguyên nhân: hàng đợi in bị kẹt do một lệnh in lỗi. Cách xử lý: dừng Print Spooler, xóa hàng đợi, khởi động lại dịch vụ, in thử trang kiểm tra thành công. Đã xác nhận với người dùng.
