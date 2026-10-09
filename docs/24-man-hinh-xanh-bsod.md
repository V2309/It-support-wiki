# Màn hình xanh chết chóc (BSOD - Blue Screen of Death)

| | |
| --- | --- |
| Cấp độ | L1 / L2 |
| Mức ưu tiên thường gặp | P2 / P3 (P2 nếu máy của lãnh đạo hoặc xảy ra liên tục không khởi động được) |
| Thời gian xử lý ước tính | 20-45 phút |
| Cần quyền quản trị | Có |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Máy tính đột ngột sập nguồn và hiện màn hình xanh thông báo lỗi: *"Your PC ran into a problem and needs to restart"*.
- Màn hình hiển thị mã lỗi (Stop Code) như:
  - `CRITICAL_PROCESS_DIED`
  - `INACCESSIBLE_BOOT_DEVICE`
  - `IRQL_NOT_LESS_OR_EQUAL`
  - `PAGE_FAULT_IN_NONPAGED_AREA`
  - `MEMORY_MANAGEMENT`
  - `KERNEL_DATA_INPAGE_ERROR`
- Kèm theo file gây lỗi (nếu có), ví dụ: `nvlddmkm.sys`, `tcpip.sys`, `ntoskrnl.exe`.
- Máy có thể bị kẹt trong vòng lặp khởi động lại liên tục (Reboot loop).

## Câu hỏi cần hỏi người dùng trước

- Sự cố xảy ra khi đang thao tác gì (mở phần mềm nặng, họp Teams, cắm thiết bị ngoài)?
- Gần đây máy có vừa cập nhật Windows, cập nhật driver hoặc cài phần mềm diệt virus mới không?
- Máy bị lỗi một lần duy nhất hay lặp lại liên tục nhiều lần trong ngày?
- Chụp lại ảnh màn hình xanh (đặc biệt là dòng **Stop code** và **What failed** nếu có).

## Kiểm tra nhanh

- Ghi lại chính xác dòng **Stop Code** và file `.sys` gặp sự cố.
- Rút toàn bộ thiết bị ngoại vi không cần thiết (USB, thẻ nhớ, dock, máy in).
- Kiểm tra xem máy có khởi động được vào chế độ an toàn (**Safe Mode**) không.

## Nguyên nhân thường gặp

1. Driver thiết bị (card màn hình, card mạng, chipset) bị xung đột hoặc lỗi thời.
2. Bản cập nhật Windows bị lỗi hoặc file hệ thống (`System32`) bị hỏng.
3. Phần cứng bị lỗi: thanh RAM lỏng/lỗi, ổ cứng SSD/HDD bị bad sector, máy quá nhiệt (thermal throttling).
4. Phần mềm diệt virus hoặc phần mềm can thiệp sâu hệ thống xung đột.

## Các bước xử lý

### Bước 1: Khởi động vào Safe Mode (Chế độ an toàn)

Nếu máy không vào được Windows bình thường:
1. Bật máy, khi thấy logo Windows xuất hiện thì giữ nút nguồn 5-10 giây để tắt cưỡng bức. Làm liên tục 2-3 lần để Windows kích hoạt màn hình **Automatic Repair**.
2. Chọn **Advanced options** > **Troubleshoot** > **Advanced options** > **Startup Settings** > Bấm **Restart**.
3. Nhấn phím `4` hoặc `F4` để vào **Enable Safe Mode** (hoặc `5` để bật Safe Mode with Networking).
- **Kết quả mong đợi:** Nếu vào được Safe Mode, nguyên nhân 90% do Driver hoặc ứng dụng bên thứ ba (không phải hỏng bo mạch chủ).

### Bước 2: Quét và sửa lỗi file hệ thống

Khi đã vào được Windows (hoặc Safe Mode), mở Command Prompt với quyền Administrator:

```cmd
sfc /scannow
DISM /Online /Cleanup-Image /RestoreHealth
```

- **Kết quả mong đợi:** Công cụ báo *"Windows Resource Protection found corrupt files and successfully repaired them"*. Khởi động lại máy kiểm tra.

### Bước 3: Gỡ bỏ Driver hoặc cập nhật vừa cài gần đây

Dựa vào mã Stop Code và file `.sys`:
- Nếu lỗi liên quan đến đồ họa (`nvlddmkm.sys`, `atikmdag.sys`): Mở **Device Manager** > **Display adapters** > Chuột phải vào card đồ họa > Chọn **Roll Back Driver** (quay về bản trước) hoặc gỡ driver và tải bản chuẩn từ trang web nhà sản xuất (Dell, HP, Lenovo).
- Nếu lỗi sau một bản cập nhật Windows: Vào **Control Panel** > **Programs and Features** > **View installed updates** > Chọn gỡ bản cập nhật vừa cài đặt gần nhất.

### Bước 4: Kiểm tra bộ nhớ RAM (Memory Diagnostic)

Nếu mã lỗi là `MEMORY_MANAGEMENT` hoặc `PAGE_FAULT_IN_NONPAGED_AREA`:
1. Mở hộp thoại Run (`Win + R`), gõ:
   ```cmd
   mdsched.exe
   ```
2. Chọn **Restart now and check for problems**.
3. Máy sẽ khởi động lại và chạy bài kiểm tra bộ nhớ RAM. Nếu màn hình báo có lỗi phần cứng (Hardware problems were detected), thanh RAM cần được vệ sinh chân cắm hoặc thay thế.

### Bước 5: Kiểm tra file Minidump (Dành cho L2)

Kiểm tra thư mục lưu vết sập hệ thống:
```text
C:\Windows\Minidump\
```
Sử dụng công cụ **BlueScreenView** hoặc **WinDbg** mở file `.dmp` gần nhất để xác định chính xác tên driver/process gây crash.

## Khi nào chuyển cấp (escalate)

- Màn hình xanh lặp lại ngay cả khi đã vào Safe Mode hoặc cài lại hệ điều hành sạch.
- Mã lỗi `INACCESSIBLE_BOOT_DEVICE` hoặc `KERNEL_DATA_INPAGE_ERROR` nghi ngờ ổ cứng SSD chết đột ngột.
- Kiểm tra RAM (`mdsched.exe`) báo lỗi phần cứng cần thay thế linh kiện.

**Thông tin đính kèm ticket:** Mã Stop Code, file `.sys` gây lỗi, ảnh chụp màn hình xanh, file `Minidump (*.dmp)`, các bước đã thực hiện.

## Phòng ngừa

- Chỉ cài đặt driver chính hãng được chứng nhận WHQL từ nhà sản xuất thiết bị.
- Vệ sinh bụi quạt tản nhiệt định kỳ để tránh máy quá nóng gây ngắt hệ thống.
- Bật tính năng tạo điểm khôi phục (System Restore Point) trước khi cài đặt phần mềm lớn.

## Mẫu ghi chú đóng ticket

> Nguyên nhân: xung đột driver card mạng không dây sau bản cập nhật tự động gây lỗi IRQL_NOT_LESS_OR_EQUAL (netwtw10.sys). Cách xử lý: khởi động vào Safe Mode, gỡ driver cũ và cài đặt driver OEM chuẩn từ trang chủ nhà sản xuất. Đã theo dõi hoạt động ổn định 2 giờ không bị sập nguồn lại.
