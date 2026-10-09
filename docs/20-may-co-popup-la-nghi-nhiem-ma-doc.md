# Máy có popup lạ, nghi nhiễm mã độc

| | |
| --- | --- |
| Cấp độ | L1 / Security |
| Thời gian xử lý ước tính | 15-60 phút |
| Cần quyền quản trị | Có |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Trình duyệt hiện popup quảng cáo, chuyển hướng website lạ.
- Máy chậm bất thường, xuất hiện phần mềm không rõ nguồn gốc.
- Antivirus/EDR cảnh báo mã độc.
- File bị đổi đuôi, không mở được hoặc có yêu cầu tiền chuộc.

## Câu hỏi cần hỏi người dùng trước

- Popup xuất hiện khi mở trang nào hoặc ứng dụng nào?
- Có vừa tải file, cài phần mềm, mở email đính kèm lạ không?
- Có dữ liệu quan trọng bị mất, bị mã hóa hoặc bị gửi ra ngoài không?

## Nguyên nhân thường gặp

1. Extension trình duyệt độc hại.
2. Phần mềm quảng cáo đi kèm bộ cài miễn phí.
3. Người dùng mở file phishing.
4. Mã độc thật sự hoặc ransomware.
5. Tài khoản bị chiếm quyền.

## Các bước xử lý

### Bước 1: Cô lập nếu có dấu hiệu nghiêm trọng

Nếu có cảnh báo EDR, file bị mã hóa, tiến trình lạ lan rộng hoặc nghi rò rỉ dữ liệu: ngắt mạng ngay (rút cáp/tắt Wi-Fi) và chuyển Security. Không tự xóa bằng tay khi cần giữ bằng chứng.

### Bước 2: Ghi nhận bằng chứng

Chụp màn hình popup/cảnh báo, ghi thời điểm, tên file đã mở, URL, email nghi ngờ. Không forward file độc hại qua email thường.

### Bước 3: Quét bằng công cụ chuẩn

Chạy Microsoft Defender hoặc EDR của công ty:

```powershell
Start-MpScan -ScanType QuickScan
```

Nếu phát hiện mã độc, làm theo playbook Security.

### Bước 4: Kiểm tra trình duyệt

- Gỡ extension lạ.
- Đặt lại search engine và trang start page.
- Xóa notification permission của website lạ.
- Xóa cache nếu cần.

### Bước 5: Kiểm tra phần mềm mới cài

Settings > Apps, sắp xếp theo ngày cài đặt. Gỡ phần mềm không được phê duyệt sau khi ghi nhận tên và nguồn.

### Bước 6: Đổi mật khẩu nếu nghi lộ tài khoản

Nếu người dùng nhập mật khẩu vào trang lạ, đặt lại mật khẩu và kiểm tra MFA theo quy trình bảo mật.

## Khi nào chuyển cấp (escalate)

- Có cảnh báo EDR/antivirus mức cao.
- File bị mã hóa hoặc nghi ransomware.
- Tài khoản bị đăng nhập lạ.
- Máy chứa dữ liệu nhạy cảm.

**Thông tin đính kèm ticket:** ảnh popup, tên file/URL/email nghi ngờ, thời điểm, kết quả quét, hành động cô lập đã làm.

## Phòng ngừa

- Bật EDR/antivirus và cập nhật tự động.
- Chặn cài extension không được phê duyệt.
- Đào tạo nhận diện phishing và phần mềm giả mạo.
- Người dùng không có quyền admin thường trực.

## Mẫu ghi chú đóng ticket

> Nguyên nhân: extension trình duyệt lạ tạo popup quảng cáo. Cách xử lý: gỡ extension, xóa quyền notification website lạ, chạy quét Defender không phát hiện mã độc, xác nhận trình duyệt hoạt động bình thường.

