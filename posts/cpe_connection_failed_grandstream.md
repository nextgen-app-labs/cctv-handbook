# Lỗi CPE Connection Failed Trên Tổng Đài Grandstream — Nguyên Nhân & Xử Lý

Lỗi **"CPE Connection Failed"** là một cảnh báo thường gặp trên hệ thống tổng đài IP Grandstream (UCM6200, UCM6300 series), đặc biệt trong quá trình sử dụng điện thoại IP Phone, bộ chuyển đổi ATA hoặc Softphone SIP. 

Nếu không xử lý kịp thời, lỗi này có thể gây gián đoạn cuộc gọi nội bộ và ngoại mạng.
![cpe-connection-failed-grandstream](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgw0STOkeNWmll8PNKhRV1_ZyGH3rMGQEFUm-fsn_hj1Y8hYJ_rJvpn8RTr6qYe2vhPdg-j9z-ZtlC11moX-BqBdJ0V1edPk7simbh7NeuN4ccmXX7FXLvxhlFJ2srs-EkH4-DuXC6ryliapTFo6wW7sOMNLfyEpHcJJvAmiCIQdINCWIglUuB29rgO-8xD/s600/L%E1%BB%97i%20CPE%20Connection%20Failed%20Tr%C3%AAn%20T%E1%BB%95ng%20%C4%90%C3%A0i%20Grandstrea.png)
---

### 1. CPE Connection Failed Là Gì?
- **CPE (Customer Premises Equipment):** Là các thiết bị đầu cuối như IP Phone, ATA (Grandstream HT801/HT802), Softphone (Wave app) hoặc VoIP Gateway.
- **Hiện tượng:** Tổng đài không thể duy trì kết nối hoặc đăng ký SIP thất bại với các thiết bị này. Lỗi thường xuất hiện trong phần **Event Logs** hoặc trạng thái Extension báo *Offline*.

---

### 2. Nguyên Nhân Thường Gặp
1. **Mất nguồn/mất mạng:** Thiết bị đầu cuối bị rút cáp LAN hoặc chưa cắm adapter.
2. **Sai thông tin SIP:** Nhập sai mật khẩu Extension, sai cổng Port hoặc sai IP SIP Server.
3. **Khác lớp mạng / NAT:** CPE và tổng đài nằm ở 2 dải VLAN khác nhau hoặc bị chặn Port.
4. **Bị chặn bởi Fail2ban:** Nhập sai mật khẩu quá số lần quy định khiến tổng đài tự động khóa IP của IP Phone.
5. **Dính tính năng SIP ALG:** Modem nhà mạng bật SIP ALG làm thay đổi gói tin SIP.
6. **Lỗi Firmware:** Firmware của IP Phone hoặc Tổng đài quá cũ.

---

### 3. Các Bước Khắc Phục Chi Tiết

#### Bước 1: Kiểm tra trên thiết bị đầu cuối (IP Phone / ATA)
- Đảm bảo thiết bị đã nhận đúng địa chỉ IP hợp lệ.
- Kiểm tra lại các thông số cấu hình SIP:
  - **SIP Server:** Nhập đúng IP của Tổng đài Grandstream.
  - **SIP User ID / Authenticate ID:** Số Extension (ví dụ: `1001`).
  - **Authenticate Password:** Mật khẩu Extension trên tổng đài.
  - **SIP Port:** `5060` (UDP).

#### Bước 2: Kiểm tra trên giao diện Web Tổng đài Grandstream
- Vào **PBX** ➔ **Extensions** để kiểm tra trạng thái đăng ký của máy nhánh.
- Vào **Maintenance** ➔ **System Events** ➔ **Event Logs** để xem chi tiết thời điểm báo lỗi.
- Vào **Security** ➔ **Fail2ban** ➔ Kiểm tra mục **Banned IPs**: Nếu thấy IP của điện thoại bị khóa, bấm **Unban (Gỡ chặn)**.

#### Bước 3: Kiểm tra Router và Cổng mạng
- Mở và định tuyến các dải port nếu dùng từ xa:
  - **SIP Port:** `5060` (UDP/TCP).
  - **RTP Voice Port:** `10000–20000` (UDP).
- **Tắt SIP ALG:** Truy cập vào Modem nhà mạng (Viettel, VNPT, FPT) tìm mục **ALG / SIP Passthrough** và chọn **Disable**.

---

### 4. Bảng Tra Cứu Xử Lý Nhanh

| Hiện tượng | Giải pháp xử lý |
| :--- | :--- |
| **IP Phone không nhận SIP** | Kiểm tra lại thông tin Extension, reset cấu hình máy nhánh |
| **Không đăng ký được từ xa qua 4G** | Bật NAT Traversal trong SIP Settings và mở port 5060, 10000-20000 |
| **IP Phone bị khóa không gửi được cuộc gọi** | Kiểm tra và xóa IP trong danh sách Fail2ban |
| **Cùng mạng LAN nhưng chập chờn** | Tắt SIP ALG trên Router, kiểm tra trùng dải IP |

> **LƯU Ý:** Khi triển khai tổng đài nội bộ, nên quy hoạch IP tĩnh cố định cho Tổng đài và các điện thoại bàn để tránh tình trạng DHCP cấp lại IP làm mất đăng ký SIP.
