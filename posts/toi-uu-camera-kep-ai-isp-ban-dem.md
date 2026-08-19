# Hướng Dẫn Tối Ưu Camera Kép (Dual Lens) & Công Nghệ Ban Đêm AI-ISP

## 1. Giới thiệu công nghệ Dual Lens & AI-ISP
Dòng camera kép tích hợp 1 ống kính góc rộng cố định và 1 ống kính quay quét (PTZ) kết hợp chip xử lý hình ảnh **AI-ISP (AI Image Signal Processor)** giúp tái tạo màu sắc chân thực trong bóng tối mà không cần bật đèn rọi gây chói mắt.

Tuy nhiên, nếu cấu hình không chuẩn, camera dễ gặp hiện tượng:
- Mất nét khi chuyển vùng quan sát giữa 2 ống kính.
- Trễ bám đuổi đối tượng (Smart Tracking Lag).
- Hình ảnh ban đêm bị bệt màu hoặc nhòe chuyển động (Motion Blur).

---

## 2. Bảng thông số khuyến nghị cấu hình ban đêm

| Thông số cài đặt | Giá trị tiêu chuẩn ban ngày | Giá trị tối ưu ban đêm (AI-ISP) | Mục đích kỹ thuật |
| :--- | :--- | :--- | :--- |
| **Màn trập (Shutter Speed)** | Auto (`1/25s` – `1/100.000s`) | Giới hạn tối thiểu `1/50s` | Tránh nhòe khi người di chuyển nhanh |
| **Chế độ màu (Day/Night)** | Auto (IR Cut) | **Full Color AI / Smart Illumination** | Tự động kích hoạt AI khử nhiễu đa khung hình |
| **Độ nhạy sáng (Gain/ISO)** | Auto | Giới hạn trần ở mức **60 – 70%** | Ngăn hiện tượng nhiễu hạt (Noise) khi thiếu sáng |
| **WDR / HDR** | Bật (Chống ngược sáng) | **Tắt hoặc hạ mức Low** | Tránh làm mờ viền đối tượng ban đêm |

---

## 3. Quy trình đồng bộ và căn chỉnh ống kính kép

### Bước 1: Đồng bộ vùng giám sát (Calibrate Tracking)
1. Đăng nhập trang quản trị camera qua trình duyệt hoặc phần mềm chuyên dụng (iVMS-4200 / SmartPSS).
2. Vào mục **PTZ Settings** > **Smart Tracking** / **Linkage Tracking**.
3. Chọn tính năng **Calibration**: Đánh dấu 3–4 điểm mốc tương ứng giữa khung hình ống kính toàn cảnh (Fixed) và ống kính chi tiết (PTZ).
4. Nhấn **Save** và kiểm tra khả năng tự động zoom khi có người đi vào vùng quét.

### Bước 2: Tối ưu thuật toán nhận diện biên (Edge AI)
- Vào mục **Smart Event** > **Intrusion / Tripwire** (Hàng rào ảo).
- Bật lọc mục tiêu: Chọn chỉ nhận diện **Human (Người)** và **Vehicle (Phương tiện)**, bỏ qua lá cây, mưa gió và động vật nhỏ.
- Cài đặt thời gian bám đuổi (**Tracking Duration**): Đặt từ **15 – 30 giây** để camera quay về vị trí giám sát mặc định sau khi đối tượng rời đi.

> **LƯU Ý:**
> - Tuyệt đối không lắp camera kép đối diện trực tiếp nguồn sáng mạnh (đèn pha, biển led) vì sẽ làm lóa cảm biến AI-ISP, khiến ống kính PTZ mất khả năng bám đuổi mục tiêu.
> - Luôn cập nhật firmware mới nhất để nhận các tập dữ liệu AI cải tiến độ chính xác nhận diện khuôn mặt và phương tiện.
