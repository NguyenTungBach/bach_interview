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

# 2. OS Command Injection
  - Là kiểu tấn công cho phép kẻ tấn công thực thi mọi lệnh trên hệ điều hành. Tương tự SQL Injection
  
```sh
// Ví dụ tấn công thông qua url bằng câu lệnh whoami
http://localhost:8000/api/cicd&&whoami
```
## 2.1 Các giải pháp
### 2.1.1 Chỉ chấp nhận đối với các giá trị được phép
### 2.1.2 Chỉ chấp nhận đầu vào chỉ có ký tự chữ và số, không có ký tự đặc biệt, khoảng trắng

# 3. Không kiểm tra Path Parameter / Directory Traversal
- Kiểu tấn công để truy cập vào vào các đường dẫn trong file, giúp kẻ tấn công tùy ý đọc các file
```sh
// Ví dụ tấn công thông qua url
https://hostname.abc/?filename=../../../etc/passwd
```

![image](https://github.com/NguyenTungBach/bach_interview/assets/78024702/814dc376-1e7a-4017-8fd0-4a9393c53339)

## 3.1 Các giải pháp
### 3.1.1 Tránh việc trực tiếp chỉ định tên tệp trong ứng dụng web thông qua tham số từ bên ngoài.
  - Ví dụ thay vì ta gọi đến file thế này
```sh
http://example.com/download.php?file=example.txt
```
  - Hãy gọi thông qua id tìm đến file
```sh
http://example.com/1
```
### 3.1.2 Khi mở tệp tin, hãy chỉ định một thư mục (directory) cố định và đảm bảo rằng tên tệp (file) không chứa tên thư mục (Directory)

# 4 Lỗi quản lý session
-  Session Id dễ đoán và dễ lấy, không có thời gian sử dụng có thể khiến kẻ tấn công lấy được thông tin (Ở đây chủ yếu nói đến là token)

## 4.1 Các giải pháp
### 4.1.1 Tạo Session ID khó đoán 
### 4.1.2 Không lưu trữ session ID trong tham số URL.
### 4.1.3 Sau khi đăng nhập thành công,  tạo một session mới 
### 4.1.4 Sau khi đăng nhập thành công, phát hành một thông tin bí mật riêng biệt khác với Session ID hiện có và kiểm tra giá trị này sau mỗi chuyển trang
### 4.1.5 Khi đặt Session ID vào Cookie, chú ý đến thiết lập thời hạn hoạt động của nó

# 5 Tấn công Cross-Site Scripting (XSS)
- Sử dụng câu lệnh java script để truy cập vào server
VD: người dùng nhập đoạn script đơn giản như sau

![image](https://github.com/NguyenTungBach/bach_interview/assets/78024702/1b2072aa-a85f-4806-8e2f-65c6057b4eb5)

Lúc đó sau khi nhấn nút “Search”, script được nhập sẽ được thực hiện.

![image](https://github.com/NguyenTungBach/bach_interview/assets/78024702/b4fd5f89-6b4a-42a8-b2e4-0e93ec88d43b)

## 5.1 Các giải pháp
### 5.1.1 Không tạo nội dung của các phần tử <script>...</script> một cách động
### 5.1.2 Không cho phép tải các tệp stylesheet từ bất kỳ trang web nào

# 6 Tấn công Cross-Site Request Forgery (CSRF)
- Kiểu tấn công giả dạng người dùng, khi người dùng tương tác một trang web không phải của bạn nhưng trang web này lại giả dạng request người dùng gửi đến trang của web của bạn. Trang web bạn nhận thấy cookie người dùng sẽ nghĩ là bình thường nhưng lại là request do hacker tạo ra.

## 6.1 Các giải pháp
### 6.1.1 Tạo Session ID khó đoán 
### 6.1.2 Sử dụng SameSite Cookies
  - Đặt cờ SameSite cho cookies để giảm nguy cơ CSRF. Cờ SameSite có thể được đặt thành "Strict" hoặc "Lax" để chỉ cho phép các yêu cầu từ cùng một trang web
