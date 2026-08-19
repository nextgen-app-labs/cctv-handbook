# Cấu Hình VLAN & QoS Chống Nghẽn Camera Trên Hạ Tầng Switch 2.5G

## 1. Nguyên nhân hệ thống Camera nhiều kênh bị giật lag
Khi nâng cấp hệ thống camera độ phân giải cao (4K/8K) kết hợp hạ tầng switch **2.5Gbps / PoE++**, các vấn đề thường gặp gồm:
- Luồng video RTSP bị nghẽn do chạy chung dải mạng với người dùng lướt web/tải file dung lượng lớn.
- Bão gói tin Broadcast làm mất kết nối ngẫu nhiên một số mắt camera (Offline tạm thời).
- Switch bị quá nhiệt hoặc rớt gói tin (Packet Loss) do chưa cấu hình **QoS (Quality of Service)**.

---

## 2. Bảng phân bổ sơ đồ VLAN và dải IP chuẩn

| Tên mạng (Network) | VLAN ID | Dải IP Subnet | Ưu tiên QoS (802.1p) | Mục đích |
| :--- | :---: | :--- | :---: | :--- |
| **VLAN Quản trị** | `VLAN 1` | `192.168.1.0/24` | 0 (Normal) | Thiết bị mạng Router, Switch |
| **VLAN Camera CCTV** | `VLAN 10` | `192.168.10.0/24` | **5 (High Priority / Video)** | Chỉ gắn NVR và Camera PoE |
| **VLAN Văn phòng/Wi-Fi**| `VLAN 20` | `192.168.20.0/23` | 2 (Low) | Điện thoại, máy tính, khách |

---

## 3. Quy trình cấu hình thực tế trên Switch Managed

### Bước 1: Tạo VLAN và cô lập cổng kết nối (Port Isolation)
1. Đăng nhập vào giao diện Switch Managed (Ruijie / TP-Link / Cisco).
2. Vào **VLAN Management** > **802.1Q VLAN** > Tạo mới `VLAN 10`.
3. Gán cổng kết nối:
   - Các port cắm camera (Port 1 – 16): Chọn **Untagged VLAN 10 (PVID 10)**.
   - Port cắm đầu ghi NVR (Port 17): Chọn **Untagged VLAN 10**.
   - Port Uplink lên Router (Port 24): Chọn **Tagged Trunk Port** (Cho phép VLAN 1, 10, 20 đi qua).

### Bước 2: Kích hoạt tính năng IGMP Snooping & QoS cho Video Stream
- **Bật IGMP Snooping trên VLAN 10:** Ngăn luồng truyền đa hướng (Multicast) từ camera tràn sang các cổng mạng văn phòng.
- **Cấu hình QoS:**
  - Chuyển chế độ ưu tiên sang **DSCP / 802.1p Priority**.
  - Đặt độ ưu tiên cho dải IP Camera `192.168.10.0/24` ở mức **DSCP 34 (AF41 - Streaming Video)** để switch luôn ưu tiên chuyển gói tin video trước khi đường truyền nghẽn.

> **LƯU Ý:**
> - Trên Router chính, chặn tính năng định tuyến chéo (Inter-VLAN Routing) giữa VLAN 20 và VLAN 10 để người dùng Wi-Fi không thể quét dò IP hay truy cập trực tiếp vào mắt camera.
> - Kỹ thuật viên bảo trì chỉ có thể truy cập đầu ghi NVR thông qua cổng dịch vụ được mở cố định hoặc qua mạng VPN nội bộ.
