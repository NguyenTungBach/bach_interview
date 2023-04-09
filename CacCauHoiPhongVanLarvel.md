## 1. Event và Listen
- Event và Listen là

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
- Route Dispatch: Tìm đến route 
- Middleware: Lọc request
- Controller: Xử lý request và các logic. Có thể trả về view hoặc Response luôn
- View: Nếu controller trả về view thì laravel sẽ render view đó trả về cho client
- Response: trả về kết quả response về cho client



## 3. Queue
- zxc

## 4. CSRF (Giả dạng request từ webside khác)
- Là cách thức tấn công bằng cách giả dạng request từ webside khác
- VD: Hacker tạo 1 trang web với form có link POST của mình. Người dùng vô tình click vào đường link của trang web đó (kèm theo Cookie của người dùng) -> Hacker có thể truy cập vào đường link không mong muốn trên trang web mà vẫn trên danh nghĩa người dùng

## 5. CSRF Token
- Dùng để định danh
- Mỗi form đều chứa 1 token ẩn phía server gắn vào. Server sẽ so sánh 2 token đó có giống với token server gừi không

## 6. Cách query trong Laravel
- Query builder tương tác với DB
```sh
$users = DB::table('users')->where('status', 1)->get();
```

- Eloquent tương tác với model
```sh
$users = User::where('status', 1)->get();
```

## 6. Middleware  trong Laravel
- Là cơ chế lọc request. Thường dùng để kiểm tra đăng nhập
