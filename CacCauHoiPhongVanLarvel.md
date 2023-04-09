# Event và Listen
- Event và Listen là

# Queue
- zxc

# CSRF (Giả dạng request từ webside khác)
- Là cách thức tấn công bằng cách giả dạng request từ webside khác
- VD: Hacker tạo 1 trang web với form có link POST của mình. Người dùng vô tình click vào đường link của trang web đó (kèm theo Cookie của người dùng) -> Hacker có thể truy cập vào đường link không mong muốn trên trang web mà vẫn trên danh nghĩa người dùng

# CSRF Token
- Dùng để định danh
- Mỗi form đều chứa 1 token ẩn phía server gắn vào. Server sẽ so sánh 2 token đó có giống với token server gừi không

# Cách query trong Laravel
- Query builder tương tác với DB
```sh
$users = DB::table('users')->where('status', 1)->get();
```

- Eloquent tương tác với model
```sh
$users = User::where('status', 1)->get();
```
