

# Cấu Hình Static Route Xem Camera Khác Lớp Mạng (Subnet)

Trong quá trình triển khai hệ thống camera, nhiều kỹ thuật viên thường gặp tình huống đầu ghi camera và thiết bị xem không nằm cùng một lớp mạng (subnet). Điều này khiến việc truy cập camera nội bộ trở nên khó khăn, đặc biệt khi không thể thay đổi IP cùng lớp hoặc bật DHCP.

Giải pháp hiệu quả trong trường hợp này là sử dụng **định tuyến tĩnh (Static Route)** – một tính năng hầu như router nào cũng hỗ trợ.

<img width="400" height="266" alt="huong-dan-xem-camera-khac-lop-mang" src="https://github.com/user-attachments/assets/e8851eb4-38eb-4cf8-a7dd-806d6c58f2e6" />

---

### 1. Vì sao cần Static Route khi xem camera khác lớp mạng?
Thông thường, nếu đầu ghi và thiết bị xem nằm trong các lớp mạng khác nhau, chúng không thể tự động “nhìn thấy” nhau. 

**Static Route** sẽ giúp “vẽ đường” cho các gói tin đi từ mạng này sang mạng kia, cho phép thiết bị ở mạng `192.168.0.x` có thể truy cập camera ở mạng `192.168.1.x`.

---

### 2. Ví dụ cấu hình thực tế

**Cấu hình đầu ghi camera:**
- **IP:** `192.168.1.xx`
- **Subnet Mask:** `255.255.255.0`
- **Gateway:** `192.168.1.1`

**Cấu hình router TP-Link (Router phụ):**
- **LAN IP:** `192.168.0.1`
- **Subnet Mask:** `255.255.255.0`

---

### 3. Các bước thiết lập Static Route

#### Bước 1: Gán IP tĩnh cho cổng WAN của Router
- **IP WAN:** `192.168.1.90` *(cùng dải mạng với đầu ghi)*
- **Subnet Mask:** `255.255.255.0`
- **Default Gateway:** `192.168.1.1`

#### Bước 2: Cấu hình định tuyến tĩnh (Static Routing)
Vào mục **Advanced** ➔ **Routing** (hoặc **Static Route**) của Router và thêm tuyến mới:
- **Destination Network (Mạng đích):** `192.168.1.0`
- **Subnet Mask:** `255.255.255.0`
- **Gateway:** `192.168.1.90` *(IP WAN đã đặt ở Bước 1)*

---

### 4. Kết quả nghiệm thu
Sau khi hoàn tất cấu hình, tất cả các thiết bị kết nối vào mạng `192.168.0.x` (điện thoại, máy tính) đều có thể kết nối và xem trực tiếp camera trong dải mạng `192.168.1.x` một cách mượt mà.

> **LƯU Ý:** Việc sử dụng Static Route giúp kết nối camera ở khác lớp mạng một cách đơn giản mà không cần thay đổi dải IP cố định của công trình hay bật DHCP làm ảnh hưởng hệ thống mạng cũ.
