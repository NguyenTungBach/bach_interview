# 1. Tấn công SQL Injection
  - Là kiểu tấn công chèn câu lệnh SQL vào hệ thống

VD: kẻ tấn công ô input trên web và truyền câu lệnh SQL dưới đây để lấy toàn bộ thông tin người dùng
```sh
SELECT * FROM users WHERE username = '' OR 1=1--' AND password = 'mypass'
```

## 1.1 Các giải pháp
### 1.1.1 Tất cả các câu lệnh SQL đều được thực hiện bằng cách sử dụng placeholders
  - abc
### 1.1.2 Khi xây dựng câu lệnh SQL bằng cách nối chuỗi, đảm bảo rằng các biến của ứng dụng được cấu trúc chính xác như các literal SQL
  - abc
### 1.1.3 Tránh truyền trực tiếp câu lệnh SQL thông qua các tham số được chuyển vào ứng dụng web
  - abc
### 1.1.4 Không hiển thị thông báo lỗi trực tiếp cho trình duyệt.
  - abc
### 1.1.5 Cấp quyền truy cập hợp lý cho tài khoản cơ sở dữ liệu.
  - abc
