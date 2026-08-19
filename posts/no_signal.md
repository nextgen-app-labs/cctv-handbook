# Xử lý Camera Mất Tín Hiệu / Đen Hình

### 1. Hiện tượng thường gặp
- Màn hình tivi / điện thoại hiển thị màu đen, báo *No Signal*, *Offline* hoặc *IPC Offline*.
- Camera không lên đèn hồng ngoại vào ban đêm.

### 2. Nguyên nhân chính
- Mất nguồn Adaptor 12V hoặc đứt đường dây điện nguồn.
- Cổng POE trên Switch hoặc Đầu ghi bị ngắt nguồn, sập tải.
- Đầu Jack BNC bị rỉ sét / hạt mạng RJ45 bấm sai chuẩn hoặc đứt ngầm.

### 3. Các bước kiểm tra thực tế
1. **Kiểm tra nguồn cấp**:
   - Dùng đồng hồ VOM đo điện áp tại chân camera (phải đủ từ 11.5V - 12.5V DC).
   - Nếu là camera POE: Kiểm tra đèn tín hiệu cổng POE trên Switch/Đầu ghi có sáng nhấp nháy không.
2. **Kiểm tra dây cáp mạng / cáp đồng trục**:
   - Dùng máy test mạng RJ45 kiểm tra thông cả 8 sợi.
   - Thử cắm một đoạn dây mạng ngắn trực tiếp từ camera vào Switch để loại trừ lỗi đường dây âm tường.
3. **Kiểm tra xung đột địa chỉ IP**:
   - Dùng phần mềm quét IP (SADP Tool, Config Tool) xem camera có nhận đúng dải IP của đầu ghi hay không.
