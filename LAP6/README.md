
Link Youtube: https://www.youtube.com/@tranthicamtu3927
# LAB 6 – CẤU HÌNH PFSENSE, ACTIVE DIRECTORY VÀ CHÍNH SÁCH TRUY CẬP

## 1. Mục tiêu
- Tìm hiểu cách triển khai tường lửa pfSense trong môi trường mạng ảo.
- Cấu hình các giao diện mạng WAN, LAN, DMZ và OPT.
- Kết hợp Windows Server 2022 và Active Directory để phục vụ quản lý, xác thực người dùng.
- Tìm hiểu cách thiết lập và kiểm tra các chính sách kiểm soát truy cập mạng.

## 2. Môi trường thực hành
- Phần mềm ảo hóa: VMware Workstation.
- Hệ điều hành: Windows Server 2022, Windows 11.
- Tường lửa: pfSense 2.9.0.
- Mô hình mạng: Các máy ảo được kết nối thông qua mạng ảo VMware.

## 3. Nội dung thực hiện
- Khởi động và kiểm tra các máy ảo phục vụ bài thực hành.
- Kiểm tra cấu hình các giao diện WAN, LAN, DMZ và OPT2 trên pfSense.
- Truy cập giao diện quản trị pfSense từ máy Windows 11.
- Kiểm tra địa chỉ IP và cấu hình mạng trên Windows Server 2022.
- Thực hiện các lệnh `ipconfig /all`, `ping` và `nslookup` để kiểm tra kết nối mạng và phân giải tên miền.
- Kiểm tra, điều chỉnh kết nối Network Adapter trong VMware.

## 4. Kết quả thực hiện
- Khởi động được pfSense và truy cập giao diện quản trị tại địa chỉ `10.6.0.1`.
- Kiểm tra được cấu hình các giao diện mạng trên pfSense.
- Windows 11 truy cập được giao diện quản trị pfSense.
- Windows Server 2022 khởi động thành công, có địa chỉ IP `192.168.30.150`.
- Lệnh `nslookup company.local` trả về địa chỉ `192.168.30.150`, tuy nhiên xuất hiện thông báo DNS timeout.
- Kiểm tra `ping` từ Windows Server đến pfSense chưa thành công, cần tiếp tục xử lý kết nối mạng ảo.

## 5. Nhận xét
Thông qua bài thực hành, em đã hiểu rõ hơn về cách tổ chức các vùng mạng trên pfSense, cấu hình địa chỉ IP và kiểm tra kết nối giữa các máy ảo. Quá trình thực hiện cũng giúp em nhận biết một số lỗi liên quan đến cấu hình Network Adapter và kết nối mạng trong VMware.

**Trạng thái:** Đã thực hiện phần cấu hình và kiểm tra mạng cơ bản; các phần chính sách truy cập, xác thực và kiểm thử còn cần tiếp tục hoàn thiện.
