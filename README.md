# LAB_AT_BMHTTT
Các bài Lab An toàn bảo mật hệ thống thông tin
link youtube: https://www.youtube.com/@tranthicamtu3927

# LAB 1 - Bắt gói tin Telnet và SSH

## 1. Thông tin sinh viên
- Họ và tên: Trần Thị Cẩm Tú
- MSSV: [Điền MSSV của bạn]
- Môn học: An toàn và Bảo mật Hệ thống Thông tin
- Bài thực hành: Lab 1 - Bắt gói tin Telnet - SSH

## 2. Nội dung thực hành
- Xây dựng môi trường thực hành trên VMware gồm:
  - Ubuntu Server: máy Server.
  - Windows 11: máy Client.
  - Kali Linux: máy phân tích lưu lượng mạng.
- Cấu hình dịch vụ Telnet trên Ubuntu Server.
- Thực hiện kết nối Telnet từ Windows Client đến Ubuntu Server.
- Bắt và phân tích lưu lượng Telnet bằng Wireshark.
- Thay đổi mật khẩu sang mật khẩu phức tạp hơn và thực hiện lại quá trình bắt gói.
- Thực hiện kết nối SSH từ Windows Client đến Ubuntu Server.
- Bắt và phân tích lưu lượng SSH bằng Wireshark.
- Tìm hiểu phương thức xác thực SSH bằng public key.

## 3. Kết quả đạt được
- Kết nối Telnet từ Windows Client đến Ubuntu Server thành công qua TCP port 23.
- Bắt được lưu lượng của phiên Telnet và lưu thành file `.pcap`.
- Sử dụng Wireshark và Follow TCP Stream để phân tích phiên Telnet.
- Quan sát được thông tin đăng nhập và mật khẩu của phiên Telnet dưới dạng plaintext.
- Sau khi đổi sang mật khẩu dài và phức tạp hơn, Wireshark vẫn có thể quan sát được mật khẩu trong lưu lượng Telnet.
- Qua thực nghiệm xác định rằng mật khẩu mạnh không khắc phục được điểm yếu của Telnet vì kênh truyền không được mã hóa.
- Kết nối SSH từ Windows Client đến Ubuntu Server thành công qua TCP port 22.
- Bắt được lưu lượng SSH và quan sát thấy nội dung phiên được mã hóa (Encrypted packet), không thể đọc trực tiếp như Telnet.
- Quan sát được một số metadata của phiên SSH như địa chỉ IP nguồn/đích, port, kích thước và chiều truyền của các gói tin.
- Tạo được cặp khóa SSH ED25519 và thực hiện quá trình đưa public key từ Client lên Server để tìm hiểu public-key authentication.

## 4. Kết luận
Qua bài thực hành, em nhận thấy Telnet và SSH đều có thể được sử dụng để truy cập máy chủ từ xa nhưng có sự khác biệt rõ rệt về bảo mật.

Telnet không mã hóa nội dung truyền trên mạng nên khi bắt được lưu lượng, Wireshark có thể khôi phục các thông tin nhạy cảm như username và password. Việc sử dụng mật khẩu phức tạp hơn không giải quyết được vấn đề này vì điểm yếu nằm ở kênh truyền.

Ngược lại, SSH sử dụng kênh truyền được mã hóa nên nội dung của phiên không thể đọc trực tiếp từ các gói tin đã bắt được. Vì vậy SSH phù hợp hơn cho việc quản trị máy chủ từ xa trong thực tế.

## 5. Các file trong Lab
- Báo cáo Lab 1 (`.docx`)
- File bắt gói Telnet lần 1 (`.pcap`)
- File bắt gói Telnet lần 2 sau khi thay đổi mật khẩu (`.pcap`)
- File bắt gói SSH (`.pcap`)
