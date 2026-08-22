# Thiết Lập Bảo Mật Camera: Kích Hoạt E2EE & Khóa Truy Cập 2FA
![bao-mat-camera-chong-hack](https://raw.githubusercontent.com/nextgen-app-labs/cctv-handbook/refs/heads/main/bao-mat-camera-chong-hack-e2ee-2fa.png)
## 1. Nguy cơ lộ lọt hình ảnh riêng tư và botnet tấn công
Đa số các vụ rò rỉ clip camera gia đình bắt nguồn từ các nguyên nhân:
- Sử dụng mật khẩu mặc định hoặc mật khẩu ngắn, dễ đoán.
- Bật tính năng **UPnP / DMZ / Mở Port (Port Forwarding)** tùy tiện trên modem, khiến camera bị quét bởi các botnet tự động.
- Chưa kích hoạt **Xác thực 2 lớp (2FA/MFA)** và **Mã hóa luồng dữ liệu đầu cuối (End-to-End Encryption - E2EE)**.

---

## 2. Bảng đối chiếu các cấp độ bảo vệ hệ thống Camera

| Cấp độ | Cấu hình kỹ thuật | Khả năng chống tấn công | Khuyến nghị áp dụng |
| :---: | :--- | :--- | :--- |
| **Cơ bản** | Đổi mật khẩu mạnh + Tắt UPnP | Ngăn chặn quét botnet tự động | Bắt buộc 100% công trình |
| **Nâng cao** | Bật 2FA + Mã hóa luồng hình ảnh E2EE | Chống lộ clip khi bị hack tài khoản | Nhà riêng, phòng ngủ, khu nhạy cảm |
| **Chuyên sâu**| Tắt P2P Cloud + Truy cập qua VPN WireGuard | Chống can thiệp từ máy chủ trung gian | Doanh nghiệp, ngân hàng, kho quỹ |

---

## 3. Các bước thiết lập phòng thủ đa lớp chuẩn kỹ thuật

### Bước 1: Kích hoạt xác thực 2 bước (2FA) trên ứng dụng Cloud
1. Mở ứng dụng di động (**EZVIZ / Imou Life / Hik-Connect / DMSS**).
2. Vào mục **Tài khoản / Cài đặt bảo mật (Account Security)**.
3. Bật tính năng **Xác thực 2 bước (Two-Factor Authentication)**: Liên kết trực tiếp qua số điện thoại hoặc ứng dụng **Google Authenticator**.

### Bước 2: Bật mã hóa luồng hình ảnh đầu cuối (E2EE / Encryption)
1. Trong cài đặt từng mắt camera trên App, tìm mục **Mã hóa hình ảnh (Video Encryption)** và bật trạng thái sang **ON**.
2. Nhập một chuỗi mật mã tùy chỉnh (Passphrase) gồm **chữ hoa, chữ thường, số và ký tự đặc biệt**.
3. Lưu lại mã khóa này an toàn. Khi chia sẻ cho điện thoại khác, bắt buộc phải nhập mã khóa này mới giải mã xem được hình ảnh.

### Bước 3: Khóa các cổng dịch vụ nhạy cảm trên Modem/Router
- Đăng nhập vào modem chính > Tắt hoàn toàn tính năng **UPnP (Universal Plug and Play)**.
- Đổi các cổng quản trị mặc định của đầu ghi:
  - **HTTP Port:** Đổi từ `80` sang cổng ngẫu nhiên (VD: `8880`).
  - **RTSP Port:** Đổi từ `554` sang cổng khác (VD: `10554`).
  - **Server/TCP Port:** Đổi từ `8000` / `37777` sang cổng dải cao.

> **LƯU Ý:**
> - Khi khách hàng muốn xem camera từ xa một cách an toàn nhất mà không dùng Cloud của hãng, hãy triển khai cài đặt **VPN Server (WireGuard hoặc Tailscale)** trực tiếp trên Router mạng.
> - Bàn giao tài khoản chính chủ cho khách; nhân viên kỹ thuật sau khi cài đặt xong phải thoát tài khoản hoặc bàn giao quyền sở hữu thiết bị (Transfer Ownership).
