# Hướng Dẫn Xóa Gán Tài Khoản (Unbind) Camera Imou & EZVIZ

## 1. Giới thiệu lỗi "Thiết bị đã được gán vào tài khoản khác"
Khi cài đặt lại camera Wi-Fi cũ hoặc camera sang tay, thông báo lỗi phổ biến nhất là:
- **EZVIZ:** *"Thiết bị đã được liên kết với tài khoản: abc***@gmail.com..."*
- **Imou Life:** *"Thiết bị đã được thêm vào tài khoản của người dùng khác..."*

> **LƯU Ý:** Nút **Reset cứng** trên thân camera chỉ có tác dụng xóa Wi-Fi và đưa cài đặt về mặc định, **KHÔNG THỂ XÓA TÀI KHOẢN CLOUD** đã liên kết trên hệ thống máy chủ của hãng.

---

## 2. Bảng so sánh các phương pháp hủy liên kết (Unbind)

| Phương pháp | Thiết bị áp dụng | Ưu điểm | Yêu cầu bắt buộc |
| :--- | :--- | :--- | :--- |
| **Gỡ trực tiếp trên App chính** | Imou / EZVIZ | Nhanh, tức thì 100% | Cần đăng nhập được vào tài khoản cũ |
| **Tự Unbind trên App qua mạng LAN** | EZVIZ / Imou Life | Tự thao tác được | Camera và điện thoại chung một mạng Wi-Fi |
| **Gửi yêu cầu hỗ trợ hãng (Portal)** | Imou / EZVIZ | Xử lý được ca dính tài khoản rác/mất số | Chụp ảnh rõ tem nhãn có số SN / QR code |

---

## 3. Quy trình thực hiện chi tiết

### Cách 1: Tự hủy gán (Unbind) bằng App EZVIZ qua mạng LAN
1. Cắm nguồn camera và cắm dây mạng LAN vào chung modem với điện thoại (hoặc kết nối điện thoại vào Wi-Fi do camera phát ra).
2. Mở ứng dụng **EZVIZ** > Bấm dấu **(+)** để quét mã QR dưới đáy camera.
3. Khi thông báo lỗi bị gán xuất hiện, bấm vào nút **"Áp dụng hủy liên kết" (Apply for Unbinding)**.
4. Nhập mật khẩu thiết bị (chính là mã **Verification Code / 6 chữ cái in hoa** dưới tem camera).
5. Nhấn **Xác nhận** để hệ thống hủy liên kết tài khoản cũ ngay lập tức.

### Cách 2: Tự hủy gán trên App Imou Life
1. Reset camera về mặc định (giữ nút Reset 10–15 giây cho đến khi đèn đỏ sáng).
2. Kết nối điện thoại với Wi-Fi nội bộ nhà mạng mà camera đang cắm dây LAN.
3. Quét mã QR thêm camera trên app **Imou Life**.
4. Khi nhận được thông báo trùng thiết bị, chọn **"Yêu cầu hủy liên kết"**.
5. Nhập **Safety Code (Mã an toàn / Device Password)** nằm trên tem camera để hoàn tất.

### Cách 3: Hủy gán qua kênh hỗ trợ kỹ thuật chính hãng
Nếu điện thoại không tìm thấy thiết bị qua mạng nội bộ:
- **Đối với EZVIZ:**
  - Truy cập cổng hỗ trợ kỹ thuật EZVIZ hoặc liên hệ tổng đài nhà phân phối (Lê Hoàng, Nhà An Toàn, Anh Nguyệt...).
  - Cung cấp: **Ảnh chụp tem chứa số Serial Number (SN)** + **Ảnh chụp hóa đơn/phiếu bảo hành (nếu có)**.
- **Đối với Imou:**
  - Gửi email yêu cầu unbind đến: `service.global@imoulife.com` hoặc gửi qua cổng hỗ trợ của nhà phân phối Dahua/Imou tại Việt Nam.
  - Nội dung: Cung cấp ảnh chụp rõ nét tem camera chứa mã QR & dãy SN.

---

## 4. Mẹo kỹ thuật xử lý tem camera bị rách / mờ số SN
- Cắm camera vào switch/modem, dùng phần mềm dò IP chuyên dụng:
  - **Hikvision / EZVIZ:** Dùng phần mềm **SADP Tool** trên máy tính để đọc thông số **Serial No.** và **Device Serial**.
  - **Dahua / Imou:** Dùng phần mềm **ConfigTool** để quét tìm địa chỉ MAC và Serial Number.
- Với EZVIZ mất mã Verification Code: Dùng SADP Tool xuất file XML nhờ NPP reset lấy lại mã xác thực.
