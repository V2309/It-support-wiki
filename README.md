# IT Support Wiki

Bộ hướng dẫn xử lý sự cố thường gặp cho Helpdesk / IT Support (L1/L2), viết bằng tiếng Việt. Mỗi bài theo cùng một khung: triệu chứng, nguyên nhân, các bước xử lý, khi nào chuyển cấp và cách phòng ngừa.

> Các bài viết dựa trên môi trường Windows 10/11 trong doanh nghiệp (Active Directory, Microsoft 365). Lệnh nào cần quyền quản trị đều được ghi chú rõ. Hãy thử trên máy ảo hoặc home lab trước khi áp dụng vào hệ thống thật.

## Mục lục (20 bài)

Trạng thái: ✅ đã viết

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

### Thiết bị

| # | Bài | Trạng thái |
| --- | --- | --- |
| 09 | [Máy in không in](docs/09-may-in-khong-in.md) | ✅ |
| 10 | [Máy tính chạy chậm](docs/10-may-tinh-chay-cham.md) | ✅ |
| 11 | [Màn hình ngoài không nhận tín hiệu](docs/11-man-hinh-ngoai-khong-nhan-tin-hieu.md) | ✅ |
| 12 | [Bàn phím hoặc chuột không hoạt động](docs/12-ban-phim-hoac-chuot-khong-hoat-dong.md) | ✅ |
| 13 | [Không có âm thanh, micro không hoạt động trong cuộc họp](docs/13-khong-co-am-thanh-micro-khong-hoat-dong.md) | ✅ |
| 14 | [Laptop không sạc hoặc pin tụt nhanh](docs/14-laptop-khong-sac-hoac-pin-tut-nhanh.md) | ✅ |

### Phần mềm và dịch vụ

| # | Bài | Trạng thái |
| --- | --- | --- |
| 15 | [Outlook không gửi hoặc nhận được thư](docs/15-outlook-khong-gui-hoac-nhan-duoc-thu.md) | ✅ |
| 16 | [Camera không hoạt động trên Teams/Zoom](docs/16-camera-khong-hoat-dong-tren-teams-zoom.md) | ✅ |
| 17 | [Không cài được phần mềm (thiếu quyền)](docs/17-khong-cai-duoc-phan-mem-thieu-quyen.md) | ✅ |
| 18 | [Windows Update báo lỗi](docs/18-windows-update-bao-loi.md) | ✅ |
| 19 | [Không truy cập được ổ đĩa chia sẻ](docs/19-khong-truy-cap-duoc-o-dia-chia-se.md) | ✅ |
| 20 | [Máy có popup lạ, nghi nhiễm mã độc](docs/20-may-co-popup-la-nghi-nhiem-ma-doc.md) | ✅ |

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
git remote add origin https://github.com/<tên-người-dùng>/it-support-wiki.git
git push -u origin main
```

Tạo repository trống (không chọn README/license) trên GitHub trước khi chạy `git remote add`. Nên bật GitHub Pages hoặc ghim repository lên hồ sơ để nhà tuyển dụng dễ thấy.

## Giấy phép

Chọn một giấy phép (ví dụ MIT hoặc CC BY 4.0) và thêm file `LICENSE` trước khi công khai.
