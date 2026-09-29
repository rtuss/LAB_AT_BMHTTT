# LAB 3 – NHẬN DIỆN VÀ ỨNG PHÓ CÁC MỐI ĐE DỌA ĐẾN AN TOÀN THÔNG TIN

## 1. Thông tin sinh viên

- Họ và tên: Trần Thị Cẩm Tú
- MSSV: 1150080162
- Lớp: 11_ĐHCNPM2
- Môn học: An toàn và Bảo mật Hệ thống Thông tin
- Lab: LAB 3 – Nhận diện và ứng phó các mối đe dọa đến an toàn thông tin

---

## 2. Mục tiêu bài LAB

Bài LAB nhằm thực hành nhận diện và phân tích các mối đe dọa phổ biến đối với hệ thống thông tin thông qua môi trường máy ảo Windows 11.

Các nội dung chính gồm:

- Xác định Asset, Vulnerability, Threat, Risk và Control.
- Kiểm tra khả năng phát hiện mẫu thử EICAR của Microsoft Defender.
- Phân tích sự kiện xác thực Windows thông qua Event ID 4624, 4625 và 4648.
- Thực hiện password rotation cho tài khoản LAB.
- Sử dụng Sysmon để giám sát tiến trình và các thay đổi hệ thống.
- Phát hiện persistence bằng Autoruns.
- Quan sát dịch vụ lắng nghe và lưu lượng mạng bằng các công cụ hệ thống/Wireshark.
- Phân tích DoS/DDoS, mail bombing và Social Engineering/Phishing trong môi trường an toàn.
- Thu thập Evidence, cleanup và kiểm tra phục hồi hệ thống.

---

## 3. Môi trường thực hành

| Thành phần | Phiên bản / Cấu hình |
|---|---|
| Virtualization | VMware Workstation |
| Guest OS | Windows 11 |
| Windows Version | 25H2 |
| OS Build | 26200.9457 |
| Network | Host-only |
| Python | 3.14.7 |
| Wireshark / TShark | 4.6.8 |
| Sysmon | 15.22 |
| Autoruns | 14.3 |
| Process Explorer | 17.14 |

Máy ảo được cấu hình Host-only nhằm giới hạn phạm vi giao tiếp mạng trong quá trình thực hành.

---

## 4. Nội dung thực hiện

### 4.1. Baseline hệ thống

Thu thập trạng thái ban đầu của:

- Hệ điều hành.
- Microsoft Defender.
- Windows Firewall.
- Cấu hình mạng.
- Danh sách tiến trình.

Kết quả cho thấy Microsoft Defender Real-time Protection và Windows Firewall đang được bật trước khi tạo các tình huống thử nghiệm.

---

### 4.2. Tình huống 1 – Asset, Vulnerability, Threat và Risk

Xây dựng Risk Register theo mô hình:

`Asset → Vulnerability → Threat → Risk → Control`

Đồng thời phân loại các nguồn đe dọa thành:

- Hành động vô ý.
- Hành động cố ý.
- Thảm họa tự nhiên.
- Lỗi kỹ thuật.
- Lỗi quản lý.

**Kết quả:** Xác định được mối quan hệ giữa tài sản, điểm yếu, mối đe dọa, rủi ro và biện pháp kiểm soát.

---

### 4.3. Tình huống 2 – EICAR và Microsoft Defender

Tạo EICAR Standard Anti-Virus Test File trong môi trường LAB để kiểm tra khả năng phát hiện của Microsoft Defender.

**Kết quả:**

- Microsoft Defender phát hiện `Virus:DOS/EICAR_Test_File`.
- File được đưa vào trạng thái `Quarantined`.
- Không tắt Defender và không tạo exclusion.

EICAR chỉ là mẫu kiểm thử antivirus, không phải malware thật.

---

### 4.4. Tình huống 3 – Password và Authentication Logging

Tạo tài khoản cục bộ `lab3user` và bật Audit Logon cho Success/Failure.

Thực hiện:

- Một lần xác thực thành công.
- Hai lần xác thực thất bại có kiểm soát.
- Phân tích Event ID 4624, 4625 và 4648.
- Đổi mật khẩu của `lab3user`.
- Kiểm chứng mật khẩu cũ bị từ chối và mật khẩu mới hoạt động.

**Kết quả:**

- Event ID 4625 ghi nhận đăng nhập thất bại.
- Event ID 4624 ghi nhận đăng nhập thành công.
- Event ID 4648 ghi nhận việc sử dụng explicit credentials.
- Password rotation được kiểm chứng thành công.

---

### 4.5. Tình huống 4 – Persistence và dịch vụ lắng nghe

Cài đặt Sysmon và thu baseline Autoruns.

Tạo các artefact persistence lành tính:

`LAB3_Run_Demo`

`LAB3_Persistence_Demo`

Sử dụng Sysmon, Autoruns và Process Explorer để quan sát và đối chiếu các dấu vết.

**Kết quả:**

- Sysmon ghi nhận Process Create bằng Event ID 1.
- Autoruns phát hiện entry persistence `LAB3_Run_Demo`.
- Các artefact LAB được phân biệt với các entry hệ thống bình thường.

---

### 4.6. Tình huống 5 – Sniffing / HTTP / HTTPS

Thực hiện capture lưu lượng trong phạm vi môi trường LAB và phân tích sự khác biệt giữa HTTP và HTTPS.

**Kết quả:** Nhận biết được dữ liệu có thể quan sát trực tiếp trên HTTP và vai trò của TLS đối với HTTPS.

---

### 4.7. Tình huống 6 – DoS / DDoS / Mail Bombing

Thực hiện bài kiểm thử tải cục bộ theo script được cung cấp, chỉ nhắm đến:

`127.0.0.1:8080`

Đồng thời phân tích các dataset offline liên quan đến DDoS và mail bombing.

**Kết quả:** Phân biệt được DoS và DDoS, đồng thời nhận diện các dấu hiệu bất thường về lưu lượng và số lượng email.

---

### 4.8. Tình huống 7 – Social Engineering / Phishing

Phân tích mẫu email phishing offline và các tình huống Social Engineering được cung cấp.

Các dấu hiệu được xem xét gồm:

- Tạo cảm giác khẩn cấp.
- Display name có vẻ đáng tin.
- Domain cần xác minh.
- Reply-To khác From.
- Yêu cầu truy cập liên kết hoặc cung cấp thông tin xác thực.

**Kết quả:** Nhận diện và phân loại được các tình huống Social Engineering, Phishing và Spear Phishing.

---

## 5. Evidence

Các bằng chứng thực hành được lưu trong:

`C:\LAB3\Evidence`

Một số bằng chứng chính:

| Evidence | Nội dung |
|---|---|
| H1 | Windows Version và cấu hình Host-only |
| H2 | Phiên bản các công cụ LAB |
| H3 | Baseline Defender và Firewall |
| H4 | Defender Protection History – EICAR |
| H5 | Event ID 4625 – lab3user |
| H6 | Sysmon Event ID 1 – Process Create |
| H7 | Autoruns – LAB3_Run_Demo |
| ... | Các bằng chứng của các tình huống tiếp theo |
| H11 | Cleanup / Recovery Verification |

Ngoài ảnh chụp màn hình, các output PowerShell và log được lưu trong thư mục `Evidence`.

---

## 6. Kết quả đạt được

Sau khi hoàn thành LAB3:

- Thiết lập được môi trường Windows 11 cô lập phục vụ thực hành an toàn.
- Kiểm tra được khả năng detection/quarantine của Microsoft Defender.
- Phân tích được các sự kiện authentication của Windows.
- Kiểm chứng được password rotation bằng Security Log.
- Sử dụng được Sysmon, Autoruns và Process Explorer để quan sát dấu vết hệ thống.
- Nhận diện được persistence và dịch vụ lắng nghe bất thường.
- Thực hành phân tích traffic HTTP/HTTPS.
- Phân biệt được DoS, DDoS và mail bombing.
- Nhận diện được các dấu hiệu Social Engineering và Phishing.
- Biết cách thu thập, lưu trữ và kiểm tra tính toàn vẹn của Evidence.
- Thực hiện cleanup và kiểm tra lại trạng thái hệ thống sau LAB.

---

## 7. Cấu trúc thư mục nộp bài

```text
LAB3/
├── README.md
├── Report/
│   └── LAB3_Report.docx
├── Evidence/
│   ├── H1_...
│   ├── H2_ToolVersions.png
│   ├── H3_Baseline_Defender_Firewall.png
│   ├── H4_ProtectionHistory_EICAR.png
│   ├── H5_Event4625.png
│   ├── H6_Sysmon_Event1.png
│   ├── H7_Autoruns_LAB3_Run_Demo.png
│   └── ...
└── Logs/
    ├── baseline_*.txt
    ├── defender_eicar.txt
    ├── auth_events_before_rotation.txt
    ├── auth_events_after_rotation.txt
    └── ...
