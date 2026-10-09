# IT Support Wiki

Bộ hướng dẫn xử lý sự cố thường gặp cho Helpdesk / IT Support (L1/L2), viết bằng tiếng Việt. Mỗi bài theo cùng một khung: triệu chứng, nguyên nhân, các bước xử lý, khi nào chuyển cấp và cách phòng ngừa.

> Các bài viết dựa trên môi trường Windows 10/11 trong doanh nghiệp (Active Directory, Microsoft 365). Lệnh nào cần quyền quản trị đều được ghi chú rõ. Hãy thử trên máy ảo hoặc home lab trước khi áp dụng vào hệ thống thật.

## Cách dùng wiki

- Dùng mục **Câu hỏi cần hỏi người dùng trước** để phân loại sự cố và xác định phạm vi ảnh hưởng.
- Làm theo các bước từ trên xuống dưới, ghi lại kết quả kiểm tra vào ticket.
- Nếu sự cố ảnh hưởng nhiều người, có dấu hiệu bảo mật, mất dữ liệu hoặc cần thay đổi hạ tầng, dừng xử lý tại máy người dùng và chuyển cấp theo mục **Khi nào chuyển cấp**.

## Mức ưu tiên tham khảo

| Mức | Khi nào dùng | Ví dụ |
| --- | --- | --- |
| P1 | Ảnh hưởng toàn công ty, ngừng dịch vụ chính hoặc nghi sự cố bảo mật nghiêm trọng | VPN toàn công ty không kết nối, ransomware, Microsoft 365 diện rộng |
| P2 | Ảnh hưởng một phòng ban, nhiều người hoặc dịch vụ quan trọng bị gián đoạn | Print server lỗi, file share phòng ban không truy cập được |
| P3 | Ảnh hưởng một người dùng, có cách xử lý tạm thời | Quên mật khẩu, máy in cá nhân không in, lỗi Outlook trên một máy |
| P4 | Yêu cầu thường, không gián đoạn công việc ngay | Cài phần mềm đã phê duyệt, tư vấn cấu hình |

## Bảng tra cứu nhanh theo triệu chứng / mã lỗi

| Dấu hiệu / Mã lỗi nhận diện | Khả năng cao | Xem bài hướng dẫn |
| --- | --- | --- |
| `169.254.x.x`, "No internet, secured" | Lỗi cấp phát DHCP / Wi-Fi | [Bài 01](docs/01-khong-vao-duoc-mang.md), [Bài 02](docs/02-wifi-ket-noi-nhung-khong-co-internet.md) |
| Ping IP được nhưng không vào được web, `NXDOMAIN` | Lỗi phân giải DNS | [Bài 04](docs/04-loi-dns.md) |
| "The referenced account is currently locked out" | Khóa tài khoản do sai pass liên tục | [Bài 06](docs/06-tai-khoan-bi-khoa-active-directory.md) |
| Màn hình xanh yêu cầu nhập khóa 48 chữ số (Recovery Key ID) | BitLocker kích hoạt sau update BIOS/TPM | [Bài 21](docs/21-khoa-bitlocker-recovery-key.md) |
| Teams báo `CAA70004`, `80090016`, màn hình trắng xóa | Lỗi cache token xác thực New Teams | [Bài 22](docs/22-microsoft-teams-bao-loi.md) |
| OneDrive hiện `Processing changes`, icon X đỏ | Lỗi kẹt cache sync hoặc file quá dài | [Bài 23](docs/23-onedrive-loi-dong-bo.md) |
| Màn hình xanh sập nguồn `CRITICAL_PROCESS_DIED`, `IRQL_...` | Xung đột driver, hỏng file Windows hoặc lỗi RAM | [Bài 24](docs/24-man-hinh-xanh-bsod.md) |
| Outlook báo `Need Password`, `Disconnected`, kẹt Outbox | Lỗi Modern Auth hoặc kẹt file OST | [Bài 15](docs/15-outlook-khong-gui-hoac-nhan-duoc-thu.md) |
| Màn hình ngoài báo "No signal", nhấp nháy | Lỗi xuất hình Windows, dock hoặc cáp | [Bài 11](docs/11-man-hinh-ngoai-khong-nhan-tin-hieu.md) |
| Windows Update báo `0x80070002`, `0x8024a105` | Cache Windows Update hỏng, dịch vụ tắt | [Bài 18](docs/18-windows-update-bao-loi.md) |
| File bị đổi đuôi lạ, popup đòi tiền chuộc, EDR báo động | Nghi nhiễm Ransomware / Mã độc | [Bài 20](docs/20-may-co-popup-la-nghi-nhiem-ma-doc.md) |

## Mục lục (24 bài)

Trạng thái: ✅ đã hoàn thiện đầy đủ

### Mạng

| # | Bài | Trạng thái |
| --- | --- | --- |
| 01 | [Không vào được mạng](docs/01-khong-vao-duoc-mang.md) | ✅ |
| 02 | [Wi-Fi kết nối nhưng không có Internet](docs/02-wifi-ket-noi-nhung-khong-co-internet.md) | ✅ |
| 03 | [VPN không kết nối](docs/03-vpn-khong-ket-noi.md) | ✅ |
| 04 | [Vào được IP nhưng không vào được tên miền (lỗi DNS)](docs/04-loi-dns.md) | ✅ |

### Tài khoản và truy cập

| # | Bài | Trạng thái |
| --- | --- | --- |
| 05 | [Quên mật khẩu](docs/05-quen-mat-khau.md) | ✅ |
| 06 | [Tài khoản bị khóa (Active Directory)](docs/06-tai-khoan-bi-khoa-active-directory.md) | ✅ |
| 07 | [Không đăng nhập được Microsoft 365](docs/07-khong-dang-nhap-duoc-microsoft-365.md) | ✅ |
| 08 | [Đổi điện thoại, không nhận mã xác thực MFA](docs/08-doi-dien-thoai-khong-nhan-ma-mfa.md) | ✅ |

### Thiết bị và phần cứng

| # | Bài | Trạng thái |
| --- | --- | --- |
| 09 | [Máy in không in](docs/09-may-in-khong-in.md) | ✅ |
| 10 | [Máy tính chạy chậm](docs/10-may-tinh-chay-cham.md) | ✅ |
| 11 | [Màn hình ngoài không nhận tín hiệu](docs/11-man-hinh-ngoai-khong-nhan-tin-hieu.md) | ✅ |
| 12 | [Bàn phím hoặc chuột không hoạt động](docs/12-ban-phim-hoac-chuot-khong-hoat-dong.md) | ✅ |
| 13 | [Không có âm thanh, micro không hoạt động trong cuộc họp](docs/13-khong-co-am-thanh-micro-khong-hoat-dong.md) | ✅ |
| 14 | [Laptop không sạc hoặc pin tụt nhanh](docs/14-laptop-khong-sac-hoac-pin-tut-nhanh.md) | ✅ |
| 21 | [Kẹt màn hình khóa BitLocker Recovery Key](docs/21-khoa-bitlocker-recovery-key.md) | ✅ |
| 24 | [Màn hình xanh chết chóc (BSOD)](docs/24-man-hinh-xanh-bsod.md) | ✅ |

### Phần mềm và dịch vụ đám mây

| # | Bài | Trạng thái |
| --- | --- | --- |
| 15 | [Outlook không gửi hoặc nhận được thư](docs/15-outlook-khong-gui-hoac-nhan-duoc-thu.md) | ✅ |
| 16 | [Camera không hoạt động trên Teams/Zoom](docs/16-camera-khong-hoat-dong-tren-teams-zoom.md) | ✅ |
| 17 | [Không cài được phần mềm (thiếu quyền)](docs/17-khong-cai-duoc-phan-mem-thieu-quyen.md) | ✅ |
| 18 | [Windows Update báo lỗi](docs/18-windows-update-bao-loi.md) | ✅ |
| 19 | [Không truy cập được ổ đĩa chia sẻ](docs/19-khong-truy-cap-duoc-o-dia-chia-se.md) | ✅ |
| 20 | [Máy có popup lạ, nghi nhiễm mã độc](docs/20-may-co-popup-la-nghi-nhiem-ma-doc.md) | ✅ |
| 22 | [Microsoft Teams báo lỗi, kẹt đăng nhập hoặc trắng màn hình](docs/22-microsoft-teams-bao-loi.md) | ✅ |
| 23 | [OneDrive báo lỗi đồng bộ, xung đột file hoặc kẹt Processing](docs/23-onedrive-loi-dong-bo.md) | ✅ |

## Cách viết một bài mới

1. Sao chép [`docs/_TEMPLATE.md`](docs/_TEMPLATE.md) thành file mới, ví dụ `docs/05-tai-khoan-bi-khoa.md`.
2. Điền đủ các mục. Mỗi bước xử lý phải kiểm tra được kết quả ("nếu ping thành công thì...").
3. Chỉ ghi lệnh bạn đã chạy thử trong home lab.
4. Cập nhật trạng thái trong mục lục phía trên.

## Đưa lên GitHub

```bash
cd it-support-wiki
git init
git add .
git commit -m "Khởi tạo IT Support Wiki với 20 bài xử lý sự cố"
git branch -M main
git remote add origin https://github.com/V2309/It-support-wiki-.git
git push -u origin main
```

Repository đã được publish tại `https://github.com/V2309/It-support-wiki-`. Nên bật GitHub Pages hoặc ghim repository lên hồ sơ để nhà tuyển dụng dễ thấy.

## Tài liệu tham khảo

- [Microsoft Learn: Active Directory PowerShell](https://learn.microsoft.com/powershell/module/activedirectory/)
- [Microsoft Learn: Microsoft Defender PowerShell](https://learn.microsoft.com/powershell/module/defender/)
- [Microsoft Learn: System File Checker and DISM](https://learn.microsoft.com/troubleshoot/windows-server/installing-updates-features-roles/system-file-checker-and-dism)
- [Microsoft Learn: Temporary Access Pass in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/authentication/howto-authentication-temporary-access-pass)
- [Microsoft Learn: Microsoft 365 admin center help](https://learn.microsoft.com/microsoft-365/admin/)

## Giấy phép

Dự án sử dụng giấy phép MIT. Xem file [`LICENSE`](LICENSE).
