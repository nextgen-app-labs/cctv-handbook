# Thiết Lập Ghi Hình Lai Hybrid: Kết Hợp NVR Cục Bộ & Cloud Storage

## 1. Tại sao cần giải pháp lưu trữ Hybrid?
Lưu trữ truyền thống phụ thuộc 100% vào ổ cứng (HDD) trong đầu ghi NVR. Khi xảy ra sự cố đột nhập, kẻ gian thường phá hủy hoặc lấy cắp đầu ghi, làm mất toàn bộ bằng chứng. 

Mô hình **Hybrid Storage** kết hợp:
- Ghi hình liên tục 24/7 chất lượng cao (**4K / H.265+**) vào ổ cứng tại chỗ.
- Tự động đẩy các đoạn video sự kiện quan trọng (báo động, nhận diện khuôn mặt, đột nhập) lên **Cloud Storage / FTP Server / S3** tức thì.

---

## 2. Bảng so sánh phương thức lưu trữ

| Tiêu chí | Lưu trữ HDD cục bộ | Đồng bộ Cloud Event | Mô hình Hybrid Storage |
| :--- | :--- | :--- | :--- |
| **Băng thông mạng chiếm dụng** | 0 Mbps (Nội mạng) | 1 – 3 Mbps khi có biến | Cực thấp, tối ưu băng thông |
| **Độ an toàn dữ liệu** | Kém (Nguy cơ bị trộm NVR) | Rất cao (Lưu trên mây) | **Tuyệt đối an toàn** |
| **Khả năng xem lại chi tiết** | Đầy đủ 24/7 từng giây | Chỉ có đoạn cắt 10–30s | Đầy đủ 24/7 + Có video dự phòng |

---

## 3. Các bước cấu hình đẩy sự kiện lên Cloud qua NVR

### Bước 1: Bật tính năng nén Smart H.265+ trên luồng phụ (Sub-stream)
1. Đăng nhập vào NVR > Vào mục **Storage** > **Video Encoding**.
2. Chọn kênh camera cần đồng bộ > Chuyển sang **Sub-stream**.
3. Cài đặt chuẩn nén **H.265+**, Frame Rate: **15 fps**, Bitrate Type: **VBR** (khoảng `512 Kbps` để truyền tải nhanh khi có sự cố).

### Bước 2: Liên kết tài khoản Cloud / FTP Server
1. Truy cập **Network** > **Advanced Settings** > **Cloud Storage** hoặc **FTP**.
2. Nhập thông số máy chủ lưu trữ (Endpoint URL, Bucket Name, Access Key / Secret Key).
3. Bật tùy chọn **Upload Alarm Video** (Tải lên video cảnh báo).
4. Thiết lập thời gian cắt video: **Pre-record (Ghi trước khi có sự kiện): 5 giây** và **Post-record: 20 giây**.

### Bước 3: Gán kích hoạt sự kiện (Linkage Action)
- Vào mục **Event** > **Smart Event** > Chọn camera cần bảo vệ.
- Trong thẻ **Linkage Method**, tích chọn **Upload to Cloud / Notify Surveillance Center**.

> **LƯU Ý:**
> - Kiểm tra kỹ gói cước băng thông Upload của đường truyền Internet tại vị trí lắp đặt; đảm bảo tốc độ Upload tối thiểu từ **20 – 30 Mbps** nếu đẩy nhiều kênh đồng thời.
> - Đặt mật khẩu mã hóa luồng dữ liệu (Stream Encryption) khi đẩy lên Cloud để chống rò rỉ hình ảnh riêng tư.
