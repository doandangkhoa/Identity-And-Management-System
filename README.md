# Hệ thống Quản lý Định danh và Xác thực Đa yếu tố (IAM/MFA)

> **Bài tập lớn** – Học phần IT3120: Phân tích và Thiết kế Hệ thống  
> **Trường Công nghệ Thông tin và Truyền thông – Đại học Bách Khoa Hà Nội**

## Giới thiệu

Hệ thống Quản lý Định danh và Truy cập (Identity and Access Management - IAM) tích hợp xác thực đa yếu tố (Multi-Factor Authentication - MFA) bằng mã TOTP.

Hệ thống hướng tới việc cung cấp:
- Cơ chế đăng nhập tập trung
- Quản lý phiên làm việc
- Kiểm soát tài khoản người dùng
- Ghi nhận nhật ký bảo mật

cho môi trường ứng dụng nội bộ hoặc ứng dụng khách tích hợp qua API.

## Thành viên nhóm 28

| STT | Họ và Tên | MSSV |
|-----|-----------|------|
| 1 | Đoàn Đăng Khoa | 20235353 |
| 2 | Nguyễn Hữu Long | 20235368 |
| 3 | Nguyễn Văn Phương | 20235403 |
| 4 | Vương Toàn Minh Hiếu | 20235330 |
| 5 | Nguyễn Xuân Đức | 20235046 |

**Giảng viên hướng dẫn:** Nguyễn Kiêm Hiếu  
**Mã lớp học:** 168500

## Các phân hệ chức năng

### 1. Quản lý Tài khoản và Phân quyền (Identity & Access)
- Tạo, cập nhật, vô hiệu hóa tài khoản
- Phân quyền RBAC (Role-based Access Control)
- Đổi mật khẩu và khôi phục mật khẩu qua Email

### 2. Quản lý Phiên làm việc (Session Management)
- Đăng nhập bằng Username + Mật khẩu
- Cấp phát JWT/Session ID có thời hạn
- Hiển thị danh sách thiết bị đang đăng nhập
- Đăng xuất (Revoke) phiên từ xa

### 3. Vòng đời Xác thực Đa yếu tố (MFA Lifecycle) — *Trọng tâm*
- Bật MFA bằng QR Code + Authenticator App
- Xác thực TOTP 6 số (thay đổi mỗi 30 giây)
- Sinh và sử dụng mã dự phòng (Recovery Codes)
- Tắt MFA (yêu cầu xác thực lại)

### 4. Quản trị An ninh và Nhật ký (Security Audit & Dashboard)
- Ghi nhật ký hành động nhạy cảm (Audit Log)
- Khóa tài khoản tự động khi nhập sai quá 5 lần
- Dashboard thống kê cho Quản trị viên

## Tác nhân hệ thống

| Tác nhân | Mô tả |
|----------|-------|
| **Người dùng cuối** | Đăng nhập, quản lý bảo mật cá nhân, bật/tắt MFA |
| **Quản trị viên** | Quản lý tài khoản, phân quyền, giám sát hệ thống (kế thừa từ Người dùng) |
| **Ứng dụng Khách** | Giao tiếp với IAM qua API để xác thực token |
| **Email/SMS Agent** | Gửi link khôi phục mật khẩu, mã OTP |

## Cấu trúc thư mục

```
Identity-And-Management-System/
├── docs/
│   ├── PT_TKHT.md          # Báo cáo phân tích và thiết kế hệ thống
│   └── class_diagram.puml  # Sơ đồ lớp (PlantUML)
└── README.md
```

## Yêu cầu phi chức năng

- **Bảo mật:** Mật khẩu hash bằng Bcrypt/Argon2 + Salt. Secret Key MFA mã hóa AES-256
- **Hiệu năng:** Phản hồi xác thực MFA < 1 giây
- **Đồng bộ:** Dung sai thời gian TOTP ±30 giây
- **Giao diện:** Responsive Design

## Quy tắc nghiệp vụ

- Mật khẩu tối thiểu 8 ký tự (chữ hoa, chữ thường, số, ký tự đặc biệt)
- Mã TOTP hiệu lực 30 giây, chỉ dùng 1 lần (chống Replay Attack)
- Tài khoản khóa tự động mở sau 30 phút hoặc Admin mở thủ công
