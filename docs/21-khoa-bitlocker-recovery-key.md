# Kẹt màn hình khóa BitLocker Recovery Key

| | |
| --- | --- |
| Cấp độ | L1 / L2 |
| Mức ưu tiên thường gặp | P2 / P3 (P2 nếu ảnh hưởng người dùng VIP hoặc nhiều máy sau đợt update BIOS) |
| Thời gian xử lý ước tính | 10-25 phút |
| Cần quyền quản trị | Có (quyền xem Recovery Key trên Entra ID / Intune / AD) |
| Cập nhật lần cuối | 2026-10-09 |

## Triệu chứng

- Máy khởi động vào màn hình xanh dương yêu cầu nhập mật mã khôi phục BitLocker (BitLocker recovery screen).
- Màn hình hiện dòng chữ: "Enter the recovery key for this drive" kèm theo **Recovery Key ID** (chuỗi 8 ký tự đầu hoặc 32 ký tự).
- Người dùng không thể vào được màn hình đăng nhập Windows.

## Câu hỏi cần hỏi người dùng trước

- Trước khi bị lỗi này, máy có vừa cập nhật BIOS/firmware hoặc cập nhật Windows không?
- Máy có đang cắm thiết bị ngoại vi nào lạ không (USB, ổ cứng ngoài, dock sạc)?
- Máy có vừa bị va đập, thay đổi linh kiện phần cứng (RAM, ổ cứng, bo mạch chủ) không?
- Ghi lại chính xác 8 ký tự đầu của **Recovery Key ID** hiển thị trên màn hình.

## Kiểm tra nhanh

- Rút toàn bộ thiết bị ngoại vi không cần thiết (USB, thẻ nhớ, dock cắm) rồi bấm `Esc` hoặc khởi động lại xem máy có bypass được không.
- Chụp ảnh màn hình BitLocker chứa mã **Recovery Key ID** để đối chiếu khi tra cứu key.
- Xác định máy thuộc quản lý của hệ thống nào: Microsoft Entra ID (Azure AD), Intune, hay Active Directory (on-premises).

## Nguyên nhân thường gặp

1. Cập nhật BIOS/UEFI hoặc firmware làm thay đổi thông số TPM (Trusted Platform Module).
2. Thiết lập Secure Boot hoặc TPM trong BIOS bị tắt hoặc bị chuyển chế độ.
3. Có thiết bị USB/ổ cứng gắn ngoài cắm vào máy lúc khởi động làm đổi thứ tự boot.
4. Thay đổi phần cứng (thay mainboard, chuyển ổ cứng sang máy khác).
5. Người dùng nhập sai mã PIN BitLocker quá số lần quy định.

## Các bước xử lý

### Bước 1: Thử khởi động lại sau khi rút thiết bị ngoại vi

- Rút tất cả USB, cáp dock sạc ngoài, ổ cứng di động.
- Tắt máy bằng cách giữ nút nguồn 10 giây, sau đó bật lại.
- **Kết quả mong đợi:** Nếu nguyên nhân do thứ tự boot, máy có thể vào thẳng Windows bình thường. Nếu vẫn hiện màn hình BitLocker, chuyển sang Bước 2.

### Bước 2: Tra cứu BitLocker Recovery Key

Kỹ thuật viên IT truy cập vào hệ thống quản lý tương ứng dựa trên loại thiết bị:

#### Trường hợp A: Máy gia nhập Microsoft Entra ID / Intune (Cloud/Hybrid)
1. Truy cập **Microsoft Intune admin center** (`https://intune.microsoft.com`) hoặc **Entra admin center** (`https://entra.microsoft.com`).
2. Vào mục **Devices** > **All devices** > Tìm theo tên máy hoặc tên người dùng.
3. Chọn thiết bị > Vào mục **Recovery keys** (hoặc **BitLocker keys**).
4. Tìm dòng có **Key ID** trùng với mã hiển thị trên màn hình máy người dùng.
5. Bấm **Show recovery key** để lấy chuỗi 48 chữ số.

#### Trường hợp B: Máy gia nhập Active Directory (On-premises)
1. Mở công cụ **Active Directory Users and Computers (ADUC)** với quyền quản trị.
2. Tìm đối tượng Computer > Mở **Properties** > Chọn tab **BitLocker Recovery**.
3. So sánh mã **Recovery Key ID** và lấy chuỗi 48 số.
4. Hoặc dùng PowerShell trên máy quản trị:
   ```powershell
   Get-ADComputer -Identity "TEN_MAY" -Properties * | Select-Object -ExpandProperty "msFVE-RecoveryPassword"
   ```

#### Trường hợp C: Tài khoản cá nhân hoặc tự quản lý
- Hướng dẫn người dùng dùng điện thoại truy cập:
  ```text
  https://account.microsoft.com/devices/recoverykey
  ```
  Đăng nhập tài khoản Microsoft đã liên kết để xem key.

### Bước 3: Hướng dẫn người dùng nhập khóa 48 chữ số

- Yêu cầu người dùng dùng cụm phím số ở hàng phím số (hoặc numpad) nhập lần lượt 48 chữ số.
- Sau khi nhập xong, nhấn **Enter**.
- **Kết quả mong đợi:** Windows khởi động thành công vào màn hình đăng nhập.

### Bước 4: Tạm ngưng (Suspend) và kích hoạt lại BitLocker để đồng bộ TPM

Nếu lỗi xảy ra sau khi update BIOS, BitLocker có thể tiếp tục hỏi key ở lần khởi động kế tiếp. Cần đồng bộ lại TPM:

Mở Command Prompt bằng quyền Administrator:
```cmd
manage-bde -protectors -disable C:
manage-bde -protectors -enable C:
```

Lệnh này tạm hoãn bảo vệ và kích hoạt lại, giúp TPM ghi nhận thông số cấu hình phần cứng mới.

## Khi nào chuyển cấp (escalate)

- Không tìm thấy Recovery Key trên cả Entra ID, Intune và Active Directory.
- Đã nhập đúng chuỗi 48 chữ số nhưng Windows báo sai key hoặc lập tức treo máy.
- Nghi ngờ ổ cứng bị lỗi vật lý hoặc chip TPM trên bo mạch chủ bị chết.

**Thông tin đính kèm ticket:** Tên máy, Serial number, Recovery Key ID (đầy đủ và 8 ký tự đầu), nguồn đã tra cứu (Intune/AD), ảnh chụp lỗi.

## Phòng ngừa

- Đảm bảo chính sách GPO / Intune bắt buộc sao lưu Recovery Key lên Cloud/AD trước khi mã hóa ổ đĩa.
- Trước khi chạy firmware/BIOS update tự động, IT nên cấu hình script tạm ngưng BitLocker (`manage-bde -protectors -disable C: -rebootcount 1`).
- Hướng dẫn người dùng không tự ý tắt TPM hoặc thay đổi thiết lập trong BIOS.

## Mẫu ghi chú đóng ticket

> Nguyên nhân: máy yêu cầu BitLocker Recovery Key sau khi cập nhật BIOS tự động. Cách xử lý: tra cứu Recovery Key 48 số trên Intune theo Key ID, hỗ trợ người dùng nhập mở khóa thành công, chạy lệnh suspend/enable BitLocker để đồng bộ lại TPM. Đã khởi động lại kiểm tra không còn hỏi key.
