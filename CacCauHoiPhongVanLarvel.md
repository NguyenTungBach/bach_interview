## 1. Event và Listen và Queue
- Event là thằng tạo sự kiện. Với các tham số truyền vào
- Listen là thằng lắng nghe sự kiện, nhận các tham số truyền vào để thực hiện một hành động nào đó
- Vì trong laravel không có khái niệm về đa luồng nên Queue là một trong những được tạo ra để xử lý đa luồng

## 2. GET và POST
- GET là phương thức truyền tham số thông qua url. (Việc truyền dữ liệu bằng url sẽ bị giới hạn nên thường dùng để lấy dữ liệu về)
- POST là phương thức truyền tham số thông qua HTTP request body (Không giới hạn việc truyền dữ liệu nên thường dùng để gửi dữ liệu lên)

## 3. Cookie và Session
- Cookie lưu trữ thông tin phía người dùng -> dễ sửa đổi do lưu phía trình duyệt ***(Clean sau khi hết thời gian)***
- Session lưu trữ thông tin phía server -> Khó sửa đổi do lưu trên server ***(Clean sau khi đóng trình duyệt)***

## 4. Localstorage, Sessionstorage và Cookie
- Localstorage lưu trữ vô thời hạn
- Sessionstorage được hủy sau khi đóng tab hoặc thoát trình duyệt
- Cookie được hủy sau khi hết hạn hoặc xóa bằng java script, php bằng hàm unset

## 5. Request lifecycle trong laravel
- Service Provider: để cấu hình và đăng ký các thành phần của ứng dụng (Cái này chỉ là đầu tiên)
- Route Dispatch: Tìm đến route 
- Middleware: Lọc request
- Controller: Xử lý request và các logic. Có thể trả về view hoặc Response luôn
- View: Nếu controller trả về view thì laravel sẽ render view đó trả về cho client
- Response: trả về kết quả response về cho client

## 6. CSRF (Giả dạng request từ webside khác)
- Là cách thức tấn công bằng cách giả dạng request từ webside khác
- VD: Hacker tạo 1 trang web với form có link POST của mình. Người dùng vô tình click vào đường link của trang web đó (kèm theo Cookie của người dùng) -> Hacker có thể truy cập vào đường link không mong muốn trên trang web mà vẫn trên danh nghĩa người dùng

## 7. CSRF Token
- Dùng để định danh
- Mỗi form đều chứa 1 token ẩn phía server gắn vào. Server sẽ so sánh 2 token đó có giống với token server gừi không

## 8. Cách query trong Laravel
- Query builder tương tác với DB
```sh
$users = DB::table('users')->where('status', 1)->get();
```

- Eloquent tương tác với model
```sh
$users = User::where('status', 1)->get();
```

## 9. Middleware  trong Laravel
- Là cơ chế lọc request. Thường dùng để kiểm tra đăng nhập

## 10. Service Provider trong Laravel
- Là trung tâm của việc khởi tạo tất cả ứng dụng trong laravel. Các package nào mà cài đặt qua composer cũng đều phải khai báo trong Service Provider

## 11. Service Container trong Laravel
- Dùng để quản lý các đối tượng và phụ thuộc (như IOC Container trong Spring boot)

## 12. Binding và Singleton trong Laravel
Cả 2 đều sử dụng để đăng ký và quản lý đối tượng
- Binding: được sử dụng để đăng ký các đối tượng và cung cấp chúng cho ứng dụng khi cần thiết. Khởi tạo mỗi lần gọi đến
- Singleton: được sử dụng để đăng ký các đối tượng và cung cấp chúng cho ứng dụng khi cần thiết. Chỉ khởi tạo một lần

## 13. Các design pattern trong Laravel
