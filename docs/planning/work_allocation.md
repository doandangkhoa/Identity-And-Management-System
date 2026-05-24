# PHÂN CÔNG NHIỆM VỤ — Identity & Management System

## CHỨC NĂNG MỚI ĐƯỢC BỔ SUNG

- **Single Sign-On (SSO) bằng OAuth2/OIDC:** Hệ thống cấp phát Token cho các app nội bộ (Kế toán, Nhân sự) thay vì chỉ là form đăng nhập thông thường.
- **Xác thực dựa trên rủi ro (Risk-Based Authentication):** Tự động phân tích IP, thiết bị, thời gian và hoạt động để quyết định xem có cần ép nhập MFA hay không.
- **Xác thực tăng cường (Step-up Authentication):** Yêu cầu MFA khi người dùng truy cập vùng dữ liệu nhạy cảm (dù đang dùng máy quen).
- **Đa phương thức MFA (Multi-factor Types):** Hỗ trợ công nghệ không mật khẩu WebAuthn (Vân tay/FaceID) bên cạnh mã 6 số TOTP truyền thống.

---

## PHÂN CÔNG NHIỆM VỤ

| # | Nhiệm vụ | Thành viên | Deadline |
| :---: | :--- | :---: | :---: |
| 1 | Sơ đồ triển khai & bổ sung thêm 1 số sơ đồ tuần tự cho chức năng mới | Khoa | 27/5 |
| 2 | Sơ đồ lớp mức chi tiết bao gồm đầy đủ các thông tin và chứa các lớp ở tầng truy cập và quản lí dữ liệu (DAM) | Phương | 28/5 |
| 3 | Sơ đồ cơ sở dữ liệu (ERD) | Long | 28/5 |
| 4 | Nguyên mẫu giao diện | Hiếu, Đức | 27/5 |
| 5 | Sơ đồ luồng tương tác | Đức, Hiếu | 30/5 |

> **Lưu ý:** Báo cáo cuối kì sẽ không bao gồm báo cáo giữa kì.

---

## CHI TIẾT NHIỆM VỤ

### 1. Sơ đồ Lớp mức chi tiết (Bao gồm DAM)

- Vẽ sơ đồ lớp mức chi tiết *(deadline: 24/5)*
- Thêm các lớp ở tầng truy cập và quản lí dữ liệu DAM:
  - Lớp `OAuth2Token` và cập nhật `ClientApplication` thành `OAuth2Client`.
  - Lớp `DeviceFingerprint` và `LoginHistory` (timestamp, user agent, IP).
  - Cấu trúc lại `MfaProfile` thành `MfaCredential` (`MfaType`, `SecretKey` với TOTP, `PublicKey` với WebAuthn).
  - Bảng trung gian `UserRole`, `RolePermission` và thêm thuộc tính `sensitivityLevel` (Mức độ nhạy cảm) vào lớp `Permission`.
  - `SecurityPolicy`: thêm thuộc tính `+ evaluateRiskLevel(device: DeviceFingerprint, history: LoginHistory)` vào `SecurityEngine` để đánh giá độ an toàn của hành vi login.

### 2. Thêm Tầng DAM vào Sơ đồ Lớp

- Vẽ thêm các lớp Repository/DAO (`UserRepository`, `MfaCredentialRepository`) và nối vào các Entity tương ứng.
- Tạo thêm các class mới DAM hoặc DAO (chương 8).

### 3. Vẽ Sơ đồ Cơ sở dữ liệu (ERD)

Chuyển đổi sơ đồ lớp vừa chốt sang dạng bảng vật lý (thêm cột Khóa chính PK, Khóa ngoại FK, đổi kiểu dữ liệu sang `VARCHAR`, `INT`, `TIMESTAMP`).

### 4. Vẽ Sơ đồ Triển khai (Deployment Diagram)

### 5. Thiết kế Nguyên mẫu Giao diện (UI Mockup)

Vẽ nháp 4 màn hình trọng điểm:

- **Cổng Đăng nhập SSO (SSO Login Gateway)**
- **Màn hình Thử thách MFA** (MFA Challenge / Step-up Auth: TOTP / Vân tay / FaceID / Recovery Code)
- **Cài đặt bảo mật MFA của User**
- **Dashboard Quản lý Session của Admin**
