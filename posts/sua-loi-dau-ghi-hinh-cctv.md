# Hướng Dẫn Sửa Các Lỗi Thường Gặp Trên Đầu Ghi Hình CCTV (DVR/NVR)

## 1. Bảng tra cứu triệu chứng & Hướng xử lý nhanh

| Triệu chứng lỗi | Nguyên nhân chính | Cách xử lý tức thì |
| :--- | :--- | :--- |
| **Kêu tiếng "bíp bíp" liên tục** | Lỗi ổ cứng (HDD), xung đột IP hoặc mất mạng | Kiểm tra cáp SATA/nguồn HDD, kiểm tra kết nối mạng |
| **Không nhận ổ cứng (No HDD)** | Nguồn hỏng, dây SATA lỏng/đứt, HDD hỏng cơ/bad | Đo nguồn 12V cấp cho đầu ghi, thay dây cáp SATA, test HDD |
| **Đầu ghi treo logo / Reset liên tục** | Nguồn yếu (tụt áp), lỗi firmware, chập tải camera | Rút hết cáp camera và HDD ra rồi bật lại, thay nguồn khác |
| **Không lên hình (Không tín hiệu HDMI/VGA)** | Sai độ phân giải màn hình, cáp hỏng, chip xuất hình lỗi | Chỉnh lại độ phân giải hiển thị qua trình duyệt (Web UI) |

---

## 2. Quy trình xử lý chi tiết từng pan bệnh

### 1. Lỗi đầu ghi không nhận ổ cứng hoặc báo lỗi HDD
- **Bước 1 (Kiểm tra nguồn):** Đo điện áp adapter đầu ghi. Nguồn 12V nhưng khi tải HDD có thể bị sụt dòng (ampere không đủ khiến đĩa từ không quay).
- **Bước 2 (Kiểm tra cáp):** Vệ sinh chân cắm cáp **SATA** và cáp nguồn ổ cứng hoặc thay dây mới.
- **Bước 3 (Định dạng lại):** Truy cập **Storage** > **Storage Device** > Chọn ổ cứng và bấm **Format / Init** (Khởi tạo).

### 2. Lỗi đầu ghi kêu "Tít... Tít..." báo động liên tục
1. Đăng nhập vào giao diện đầu ghi qua màn hình trực tiếp hoặc trình duyệt.
2. Vào mục **Configuration** > **Event** > **Exceptions** (Ngoại lệ).
3. Kiểm tra các mục cảnh báo:
   - **HDD Full / HDD Error** (Lỗi lưu trữ).
   - **IP Address Conflicted** (Trùng địa chỉ IP nội mạng).
   - **Network Disconnected** (Mất kết nối mạng LAN).
4. Tắt tùy chọn **Audible Warning** (Cảnh báo âm thanh) nếu cần ngắt tiếng kêu tạm thời để xử lý.

### 3. Lỗi đầu ghi khởi động lại liên tục (Reboot Loop)
- Rút toàn bộ **jack camera (BNC hoặc cáp LAN PoE)** và **cáp nguồn ổ cứng**.
- Khởi động lại chỉ với main đầu ghi:
  - Nếu đầu ghi lên bình thường: Lần lượt cắm lại HDD rồi đến từng camera để tìm thiết bị gây chạm chập/sụt áp.
  - Nếu vẫn treo/reset: Cần nạp lại **Firmware cứu hộ (qua TFTP/UART)** hoặc thay nguồn 12V công suất cao hơn.

---

## 3. Khắc phục lỗi màn hình không nhận tín hiệu (Out of Range)

> **LƯU Ý:** Khi cắm đầu ghi vào màn hình cũ báo lỗi **"Signal Out of Range"** hoặc màn hình đen ngòm:
> 1. Dùng máy tính truy cập địa chỉ IP của đầu ghi qua trình duyệt.
> 2. Vào **System Settings** > **Menu Output** / **Display Output**.
> 3. Hạ độ phân giải xuất hình về mức an toàn: **1024x768** hoặc **1920x1080 (1080P)** rồi bấm **Save**.

---

## 4. Checklist bảo trì chống lỗi định kỳ
- Sử dụng đúng **ổ cứng chuyên dụng camera (WD Purple, Seagate SkyHawk)**, không dùng ổ PC thông thường.
- Luôn cắm đầu ghi qua **Bộ lưu điện (UPS)** hoặc ổn áp để tránh sốc điện làm lỗi bo mạch và phân vùng ổ cứng.
