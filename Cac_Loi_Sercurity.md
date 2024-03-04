# 1. Tấn công SQL Injection
  - Là kiểu tấn công chèn câu lệnh SQL vào hệ thống

VD: kẻ tấn công ô input trên web và truyền câu lệnh SQL dưới đây để lấy toàn bộ thông tin người dùng
```sh
SELECT * FROM users WHERE username = '' OR 1=1--' AND password = 'mypass'
```

## 1.1 Các giải pháp
### 1.1.1 Tất cả các câu lệnh SQL đều được thực hiện bằng cách sử dụng placeholders
  - Truyền vào bằng cách thêm placeholders không định danh hoặc placeholders định danh tránh truyền trực tiếp câu lệnh. Trong laravel là eloquent

```sh
// Ví dụ code thông thường
$stmt = $conn->prepare('INSERT INTO users (name, email, age) values (?, ?, ?)');
$stmt = $conn->prepare('INSERT INTO users (name, email, age) values (:name, :mail, :age)');
```

```sh
// Ví dụ dùng eloquent
$name = request()->get('name');
User::where("name",$name)
```
### 1.1.2 Khi xây dựng câu lệnh SQL bằng cách nối chuỗi, đảm bảo rằng các biến của ứng dụng được cấu trúc chính xác như các literal SQL
  - **Giống 1.1.1**
### 1.1.3 Không hiển thị thông báo lỗi trực tiếp cho trình duyệt.
  - giảm thiểu kẻ tấn công biết lỗi truyền SQL
### 1.1.5 Cấp quyền truy cập hợp lý cho tài khoản cơ sở dữ liệu.
  - Chỉ cho phép tài khoản người dùng truy cập vào phạm vi cơ sở dữ liệu cho phép. Ví dụ phân quyền
