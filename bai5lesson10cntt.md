#  Smart-Farm: Hệ thống Tưới Lan Tự Động IoT
##  Hướng dẫn cài đặt
Để chạy chương trình và cấu hình hệ thống trên thiết bị, bạn hãy mở terminal trong VS Code và gõ các lệnh sau:
```bash
 Cập nhật các gói phần mềm và tải mã nguồn dự án
sudo apt update && sudo apt install -y python3-pip git
git clone [https://github.com/trang-trai-lan/smart-farm-iot.git](https://github.com/trang-trai-lan/smart-farm-iot.git)
cd smart-farm-iot
 Cài đặt thư viện cần thiết và chạy chương trình
pip3 install -r requirements.txt
python3 main.py
 Tính năng chính của hệ thống[x] Tự động đọc dữ liệu độ ẩm đất và không khí liên tục[x] Bật/tắt máy bơm nước từ xa qua giao diện[ ] Tích hợp camera AI nhận diện sâu bệnh (Đang làm thêm)[x] Cảnh báo bằng còi khi nhiệt độ ngoài trời quá cao Bảng thông số kỹ thuật linh kiệnTên linh kiệnModel / Thông sốNhiệm vụ chính trong mạchVi điều khiển (SoC)ESP32 Wi-FiBộ não trung tâm, xử lý dữ liệu và kết nối mạngCảm biến độ ẩm đấtCapacitive Sensor v1.2Kiểm tra độ ẩm của giá thể trồng lanCảm biến môi trườngDHT22Đo chính xác nhiệt độ và độ ẩm không khíMạch điều khiểnRelay 5V 1-ChannelCông tắc điện tử đóng/mở máy bơm nước Chu kỳ thực thi lệnh tưới lan của CPU (Fetch – Decode – Execute)Khi hệ thống ra lệnh tưới nước, CPU sẽ trải qua 3 bước rất nhanh như sau:Fetch (Nạp lệnh): CPU lấy chỉ thị bật máy bơm từ bộ nhớ flash ra để chuẩn bị xử lý.Decode (Giải mã lệnh): Bộ phận giải mã sẽ đọc xem câu lệnh này muốn làm gì (xác định là cần kích hoạt chân GPIO nối với Relay).Execute (Thực thi): Gửi một dòng điện tín hiệu (HIGH) ra chân GPIO để đóng mạch Relay, khiến máy bơm nước khởi động tưới cho lan.
 Mô hình DIKW (Chuyển hóa dữ liệu thành hành động)Quy trình hệ thống xử lý thông tin từ lúc nhận cảm biến đến khi tưới cây:Data (Dữ liệu thô): Cảm biến trả về con số đơn thuần như 38.5 và 85.Information (Thông tin): Gắn thêm ý nghĩa cho số liệu: Nhiệt độ là 38.5°C và Độ ẩm là 85%.Knowledge (Tri thức): Phân tích tình hình: Trời đang nóng và khô, lan rất dễ bị mất nước.Wisdom (Trí tuệ / Hành động): Ra quyết định tự động: Bật ngay hệ thống phun sương để hạ nhiệt và tưới ẩm cho cây kịp thời.⚠️ Lưu ý xử lý sự cố (Khi RAM bị đầy nhật ký - Log)Nếu thiết bị chạy lâu ngày bị đầy bộ nhớ RAM do file log ghi quá nhiều, hệ thống có thể bị treo. Cách xử lý an toàn là:Khởi động lại thiết bị hoặc ngắt nguồn tạm thời.Kết nối vào terminal và dùng lệnh để xóa bớt log cũ:Bashsudo rm -rf /var/log/smart-farm/*.log
Sửa lại mức độ ghi log trong code thành WARNING để giảm tải cho RAM ở các lần chạy sau.

