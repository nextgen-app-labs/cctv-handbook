# Hướng Dẫn Mở Rộng Dải IP Trên Modem WiFi Lên 500 – 1000 Thiết Bị
![mo-rong-dai-ip] (https://raw.githubusercontent.com/nextgen-app-labs/cctv-handbook/refs/heads/main/huong-dan-mo-rong-dai-ip.jpg)
## 1. Giới thiệu & Nguyên nhân cần mở rộng IP
Mặc định, đa số modem nhà mạng cấp lớp mạng **/24 (Subnet Mask: 255.255.255.0)** chỉ cung cấp tối đa **254 địa chỉ IP** khả dụng. 

Khi thi công các hệ thống lớn như:
- Khách sạn, nhà hàng, quán café, quán game.
- Văn phòng công ty, nhà xưởng có nhiều thiết bị **IoT / Smartphone / Laptop**.

Hệ thống sẽ nhanh chóng rơi vào tình trạng **cạn kiệt IP (DHCP Exhaustion)**, dẫn đến lỗi thiết bị không nhận được IP, xoay vòng kết nối hoặc xung đột IP liên tục.

---

## 2. Bảng tra cứu & So sánh các dải Subnet phổ biến

| Subnet Mask | Prefix | Gateway IP mẫu | Dải cấp DHCP khả dụng | Tổng số IP sử dụng |
| :--- | :---: | :--- | :--- | :---: |
| `255.255.255.0` | **/24** | `192.168.1.1` | `192.168.1.2` – `192.168.1.254` | **254** |
| `255.255.254.0` | **/23** | `192.168.0.1` | `192.168.0.2` – `192.168.1.254` | **510** |
| `255.255.252.0` | **/22** | `192.168.0.1` | `192.168.0.2` – `192.168.3.254` | **1022** |

---

## 3. Các phương pháp triển khai thực tế

### Cách 1: Đổi trực tiếp Subnet Mask trên Modem (Tối ưu nhất nếu modem hỗ trợ)
- **Ưu điểm:** Tận dụng thiết bị sẵn có, không phát sinh chi phí phần cứng.
- **Nhược điểm:** Nhiều dòng modem nhà mạng (ZTE, Huawei, Dasan) bị khóa tính năng đổi Subnet.

### Cách 2: Chuyển Modem sang Bridge Mode & Dùng Router cân bằng tải
- **Áp dụng:** Khi modem nhà mạng không hỗ trợ đổi Subnet hoặc chịu tải kém (dưới 50–70 user).
- **Cách làm:** Cấu hình modem chính chạy **Bridge Mode**, quay PPPoE và cấp DHCP qua Router chuyên dụng (**MikroTik, DrayTek, TP-Link Omada**).

### Cách 3: Chia VLAN cách ly (Khuyên dùng cho hệ thống chuyên nghiệp)
- Giúp cô lập gói tin quảng bá, chia tách luồng mạng văn phòng, khách vãng lai và hệ thống camera nội bộ.
  - **VLAN 10 (Nội bộ):** `192.168.10.0/24` (254 IP)
  - **VLAN 20 (Khách/Guest):** `192.168.20.0/23` (510 IP)

---

## 4. Hướng dẫn chi tiết cấu hình Subnet Mask

### Trường hợp A: Cấu hình dải Subnet /23 (Cấp tối đa 510 IP)
1. Đăng nhập vào trang quản trị modem (thường là `192.168.1.1` hoặc `192.168.0.1`).
2. Tìm đến mục **Network** > **LAN** / **DHCP Server Settings**.
3. Thiết lập thông số:
   - **IP Address (Gateway):** `192.168.0.1`
   - **Subnet Mask:** `255.255.254.0`
   - **DHCP Start IP:** `192.168.0.2`
   - **DHCP End IP:** `192.168.1.254`
   - **Lease Time:** Đặt từ **2 – 4 giờ** (cho quán ăn/cafe) để giải phóng IP nhanh.
4. Nhấn **Save / Apply** và khởi động lại modem.

### Trường hợp B: Cấu hình dải Subnet /22 (Cấp tối đa 1022 IP)
1. Truy cập mục cấu hình **LAN / DHCP Server**.
2. Thiết lập thông số:
   - **IP Address (Gateway):** `192.168.0.1`
   - **Subnet Mask:** `255.255.252.0`
   - **DHCP Start IP:** `192.168.0.2`
   - **DHCP End IP:** `192.168.3.254`
3. Lưu cấu hình và tiến hành kiểm tra kết nối.

> **LƯU Ý:**
> - Khi đổi Subnet sang `/23` hoặc `/22`, bắt buộc phải đổi IP Gateway về `192.168.0.1` (hoặc dải bắt đầu tương ứng) để tránh lỗi lệch dải mạng.
> - Sau khi lưu cấu hình, máy tính cấu hình có thể bị ngắt kết nối tạm thời; cần rút cáp cắm lại hoặc bật/tắt Wi-Fi để nhận IP mới.

---

## 5. Cảnh báo kỹ thuật & Tối ưu hiệu năng

- **Bão Broadcast (Broadcast Storm):** Càng nhiều thiết bị trong cùng 1 lớp mạng phẳng (Flat Network) thì lưu lượng broadcast càng lớn, dễ gây nghẽn mạng và đơ router.
- **Bảo mật & Ổn định:**
  - Với mạng trên 300 client, bắt buộc nên dùng **Router chuyên dụng** và chia **VLAN**.
  - Bật tính năng **DHCP Snooping** và **ARP Inspection** trên Switch Managed để chống thiết bị cắm nhầm cấp ngược DHCP.

---

## 6. Câu hỏi thường gặp (FAQ)

- **Q: Tại sao đặt Subnet Mask `255.255.254.0` mà dải IP lại có cả `.0.x` và `.1.x`?**  
  *A:* Vì với Prefix `/23`, 1 bit của Octet thứ 3 được mượn làm phần Host, gộp chung 2 dải `192.168.0.x` và `192.168.1.x` thành một mạng duy nhất mà không cần định tuyến.

- **Q: Modem nhà mạng bị ẩn/khóa ô đổi Subnet Mask thì xử lý thế nào?**  
  *A:* Hãy chuyển modem về chế độ **Bridge Mode** và lắp thêm Router chịu tải chuyên dụng như MikroTik hEX / RB750Gr3.
