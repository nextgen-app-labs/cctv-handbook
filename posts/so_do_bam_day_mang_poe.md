# Sơ Đồ Bấm Dây Mạng RJ45, Nguồn PoE & Đấu Nối Camera Toàn Tập

Trong quá trình thi công camera quan sát và hệ thống mạng, việc nắm vững thứ tự màu dây mạng, phân bổ chân nguồn PoE, cũng như cách đấu nối Jack BNC, Micro thu âm và cổng RS485 là kỹ năng cơ bản nhưng tối quan trọng để đảm bảo tín hiệu thông suốt và an toàn cho thiết bị.
![so-do-bam-day-mang-chuan](https://raw.githubusercontent.com/nextgen-app-labs/cctv-handbook/refs/heads/main/huong-dan-bam-day-mang-chuan.jpg)
---

## 1. Sơ Đồ Bấm Dây Mạng Chuẩn T568B & T568A

Đầu hạt mạng RJ45 chuẩn có **8 chân tiếp xúc (Pin 1 đến Pin 8)** được đánh số từ **Trái qua Phải** khi nhìn vào mặt dưới (mặt chân đồng hướng lên trên, lẫy gài hướng xuống dưới).

### Bảng màu so sánh chuẩn Chuẩn B (T568B) và Chuẩn A (T568A):

| Chân (Pin) | Chuẩn B (T568B) - Phổ biến tại VN | Chuẩn A (T568A) - Quốc tế | Chức năng (100Mbps) |
| :---: | :--- | :--- | :--- |
| **Pin 1** | 🟠⚪ **Trắng Cam** | 🟢⚪ **Trắng Xanh Lá** | Truyền Data (TX+) |
| **Pin 2** | 🟠 **Cam** | 🟢 **Xanh Lá** | Truyền Data (TX-) |
| **Pin 3** | 🟢⚪ **Trắng Xanh Lá** | 🟠⚪ **Trắng Cam** | Nhận Data (RX+) |
| **Pin 4** | 🔵 **Xanh Dương** | 🔵 **Xanh Dương** | Nguồn PoE (+) / Dự phòng |
| **Pin 5** | 🔵⚪ **Trắng Xanh Dương** | 🔵⚪ **Trắng Xanh Dương** | Nguồn PoE (+) / Dự phòng |
| **Pin 6** | 🟢 **Xanh Lá** | 🟠 **Cam** | Nhận Data (RX-) |
| **Pin 7** | 🟤⚪ **Trắng Nâu** | 🟤⚪ **Trắng Nâu** | Nguồn PoE (-) / Dự phòng |
| **Pin 8** | 🟤 **Nâu** | 🟤 **Nâu** | Nguồn PoE (-) / Dự phòng |

### 📌 Khi nào dùng bấm thẳng và bấm chéo?
* **Bấm Cáp Thẳng (Straight-Through):** Cả 2 đầu bấm cùng chuẩn **B - B** (hoặc A - A). Dùng kết nối giữa các thiết bị khác loại: *Camera -> Switch, Máy tính -> Router/Modem, Đầu ghi NVR -> Switch.* (99% công trình dùng chuẩn B - B).
* **Bấm Cáp Chéo (Crossover):** 1 đầu chuẩn **A**, 1 đầu chuẩn **B**. Dùng kết nối trực tiếp giữa 2 thiết bị cùng loại không có tính năng Auto-MDIX: *Máy tính -> Máy tính, Switch cũ -> Switch cũ.*

---

## 2. Sơ Đồ Phân Bổ Chân Nguồn PoE (Power over Ethernet)

Hệ thống Camera IP PoE sử dụng 2 cơ chế cấp nguồn chính qua cáp mạng:

### A. Chuẩn PoE Chuẩn Quốc Tế IEEE 802.3af / 802.3at / 802.3bt (48V)
* **Mode A (Endspan):** Nguồn điện 48V đi chung với dây truyền tín hiệu Data trên **4 chân: 1, 2 (+), 3, 6 (-)**. 4 chân còn lại không cấp nguồn.
* **Mode B (Midspan / Injector):** Nguồn điện đi riêng trên **4 chân trống: 4, 5 (+) và 7, 8 (-)**.

### B. Chuẩn Passive PoE (12V - 24V Thường Dùng Cho Bộ Thu Phát WiFi / Camera Dân Dụng)
* **Chân 1, 2, 3, 6:** Truyền dữ liệu Internet (Data 100Mbps).
* **Chân 4, 5 (Cặp Xanh Dương):** Dương nguồn điện `DC (+)`.
* **Chân 7, 8 (Cặp Nâu):** Âm nguồn điện `DC (-) / Mass`.

> **💡 Mẹo thợ thực chiến: Chạy 2 Camera IP trên 1 sợi cáp mạng 8 lõi**
> - Chuẩn mạng 100Mbps của Camera IP chỉ cần **4 sợi: 1, 2, 3, 6** để truyền tín hiệu.
> - Nếu kéo dây quá khó khăn, bạn có thể tách:
>   - **Cam 1:** Bấm 4 sợi *Trắng Cam, Cam, Trắng Xanh Lá, Xanh Lá* vào chân **1, 2, 3, 6**.
>   - **Cam 2:** Bấm 4 sợi *Trắng Xanh Dương, Xanh Dương, Trắng Nâu, Nâu* vào chân **1, 2, 3, 6** ở cả 2 đầu.

---

## 3. Sơ Đồ Đấu Nối Camera Analog (Cáp Đồng Trục RG59/RG6)

### Sơ đồ Jack BNC & Nguồn DC 12V:
1. **Jack BNC (Tín hiệu hình ảnh):**
   - **Lõi đồng chính giữa (Center Conductor):** Nối vào chốt dương (+) của Jack BNC (Tín hiệu Video).
   - **Lớp lưới giáp kim loại (Shield Braid):** Nối vào vỏ bọc/kẹp âm (-) của Jack BNC (Chống nhiễu & Mass).
2. **Jack Nguồn DC 12V:**
   - **Dây Đỏ:** Dương nguồn `+12V DC` (Chân giữa của Jack cái/đực).
   - **Dây Đen:** Âm nguồn `GND / Mass` (Vỏ ngoài của Jack).

---

## 4. Sơ Đồ Đấu Nối Micro Thu Âm Cho Camera

Micro thu âm camera thường có 3 dây ra (hoặc 1 đầu hoa sen RCA + 1 đầu jack nguồn DC):
* **Dây Đỏ (Power +):** Nối vào nguồn `+12V DC`.
* **Dây Trắng / Vàng (Audio Out):** Nối vào chân Audio In (RCA) của Đầu ghi / Camera.
* **Dây Đen (GND / Mass):** Nối chung âm nguồn `-12V` và âm của đường Audio.

---

## 5. Sơ Đồ Đấu Cổng RS-485 Điều Khiển PTZ

Dùng điều khiển xoay quét và Zoom cho các dòng Camera Speed Dome Analog / Bàn điều khiển:
* **Cực `A+` (hoặc `D+`, `TX+`):** Nối với cực `A+` trên đầu ghi hoặc bàn phím điều khiển.
* **Cực `B-` (hoặc `D-`, `TX-`):** Nối với cực `B-` trên đầu ghi hoặc bàn phím điều khiển.
* Sử dụng dây xoắn đôi (Twisted Pair) để chống nhiễu trên đường truyền xa lên đến 1200 mét.
