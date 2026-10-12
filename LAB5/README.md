LAB5 – CẤU HÌNH VÀ KIỂM THỬ TƯỜNG LỬA pfSense
Các bài Lab An toàn bảo mật hệ thống thông tin link youtube: https://www.youtube.com/@tranthicamtu3927

1. Thông tin sinh viên
Họ và tên: Trần Thị Cẩm Tú
MSSV: 1150080162
Lớp: 11_ĐHCNPM2
Môn học: An toàn và Bảo mật Hệ thống Thông tin
Lab: LAB5 – CẤU HÌNH VÀ KIỂM THỬ TƯỜNG LỬA pfSense

2. Giới thiệu

Bài thực hành LAB5 thuộc học phần An toàn và Bảo mật Hệ thống Thông tin, tập trung vào việc triển khai và cấu hình tường lửa pfSense nhằm kiểm soát lưu lượng mạng giữa các vùng WAN, LAN và DMZ.

Bài thực hành được thực hiện trên môi trường máy ảo VMware Workstation, giúp tìm hiểu cách hoạt động của firewall rule, NAT và cách kiểm tra khả năng cho phép hoặc ngăn chặn các kết nối mạng.
2. Mục tiêu thực hành

Cài đặt và cấu hình tường lửa pfSense.

Xây dựng mô hình mạng gồm WAN, LAN và DMZ.

Cấu hình địa chỉ IP và kết nối mạng giữa các máy ảo.

Thiết lập các firewall rule để kiểm soát lưu lượng mạng.

Kiểm thử các tình huống cho phép và chặn kết nối.

Quan sát kết quả bằng lệnh ping và Firewall Log.

3. Môi trường thực hành

Thành phần

Vai trò

VMware Workstation

Phần mềm tạo và quản lý máy ảo

pfSense Community Edition

Tường lửa quản lý WAN, LAN và DMZ

Windows 11

Máy thuộc LAN, quản trị pfSense và kiểm thử

Ubuntu Server

Máy thuộc DMZ, kiểm thử kết nối mạng

Cấu hình mạng sử dụng

Vùng mạng

Địa chỉ IP

Vai trò

WAN

192.168.211.0/24

Kết nối mạng bên ngoài

LAN

192.168.13.0/24

Mạng nội bộ

DMZ

192.168.20.0/24

Vùng mạng tách biệt

Windows 11

192.168.13.10

Máy kiểm thử LAN

Ubuntu Server

192.168.20.10

Máy kiểm thử DMZ

Các địa chỉ trên được ghi nhận trong quá trình thực hành và kiểm thử.

4. Nội dung thực hành

4.1. Cài đặt và cấu hình pfSense

Khởi tạo máy ảo pfSense trên VMware Workstation.

Cấu hình các card mạng tương ứng với WAN, LAN và DMZ.

Thiết lập địa chỉ IP cho các vùng mạng.

Truy cập giao diện quản trị pfSense từ Windows 11.

Kiểm tra kết nối mạng và cấu hình firewall rule.

4.2. Tình huống 1 – Chặn ICMP nhưng vẫn cho phép Web/DNS

Mục tiêu: Tìm hiểu cách sử dụng firewall rule để chặn một giao thức cụ thể mà vẫn cho phép các dịch vụ cần thiết hoạt động.

Nội dung:

Cấu hình rule chặn lưu lượng ICMP.

Cấu hình rule cho phép lưu lượng Web/DNS.

Kiểm thử kết nối để đánh giá hoạt động của các rule.

4.3. Tình huống 2 – Chỉ cho một host cụ thể ra Internet

Mục tiêu: Kiểm soát quyền truy cập Internet dựa trên địa chỉ IP nguồn.

Nội dung:

Cấu hình firewall rule cho phép một host được truy cập Internet.

Hạn chế các host không thuộc phạm vi cho phép.

Kiểm thử kết nối và đánh giá kết quả.

4.4. Tình huống 3 – Cô lập DMZ khỏi LAN

Mục tiêu: Ngăn chặn các kết nối không được phép từ DMZ vào mạng LAN, đồng thời duy trì khả năng truy cập Internet của DMZ.

Nội dung thực hiện:

Cấu hình Ubuntu Server với địa chỉ IP 192.168.20.10/24.

Kiểm tra kết nối đến gateway 192.168.20.1.

Kiểm tra kết nối Internet đến 1.1.1.1.

Tạo firewall rule Block DMZ to LAN trên pfSense.

Đặt rule Block phía trên rule Allow DMZ to Internet.

Bật chức năng ghi log cho rule Block.

Kiểm thử kết nối từ Ubuntu Server đến Windows 11.

Kiểm tra Firewall Log để xác nhận kết quả.

Kết quả kiểm thử:

Nội dung kiểm thử

Kết quả

Ubuntu ping gateway 192.168.20.1

Thành công

Ubuntu ping 1.1.1.1

Thành công

Ubuntu ping Windows 11 khi rule Block hoạt động

Thất bại, mất 100% gói tin

Kiểm tra Firewall Log

Ghi nhận gói ICMP bị chặn

Kiểm tra Internet từ Ubuntu sau khi chặn LAN

Thành công

Nhận xét:

Kết quả cho thấy pfSense có thể kiểm soát lưu lượng giữa các vùng mạng thông qua firewall rule. Khi rule Block DMZ to LAN được kích hoạt, các gói ICMP từ Ubuntu Server đến Windows 11 bị chặn và được ghi nhận trong Firewall Log. Trong khi đó, Ubuntu Server vẫn có thể truy cập Internet.

5. Kết quả đạt được

Sau khi thực hiện LAB5, đã đạt được các kết quả sau:

Triển khai được môi trường thực hành pfSense trên VMware Workstation.

Thiết lập mô hình mạng gồm ba vùng WAN, LAN và DMZ.

Truy cập và sử dụng được giao diện quản trị pfSense.

Thực hành cấu hình firewall rule để kiểm soát kết nối mạng.

Thực hiện kiểm thử các tình huống firewall trong phạm vi bài thực hành.

Xác nhận khả năng cô lập DMZ khỏi LAN thông qua kết quả ping và Firewall Log.

Hiểu rõ hơn vai trò của firewall rule, NAT và việc phân chia các vùng mạng trong bảo mật hệ thống.

6. Kết luận

Thông qua LAB5, em đã hiểu rõ hơn nguyên lý hoạt động của tường lửa pfSense và cách sử dụng firewall rule để quản lý lưu lượng mạng.

Bài thực hành giúp em làm quen với việc phân chia mạng thành các vùng WAN, LAN và DMZ, kiểm thử kết nối, xác định nguyên nhân kết nối bị chặn và sử dụng Firewall Log để theo dõi hoạt động của tường lửa.

Đặc biệt, kết quả kiểm thử tình huống cô lập DMZ khỏi LAN cho thấy việc cấu hình đúng firewall rule và thứ tự xử lý rule có vai trò quan trọng trong việc bảo vệ mạng nội bộ.
