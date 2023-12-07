# Sơ qua các bước
- B1: Cấu hình đăng ký slack
- B2: Tạo laravel và code
- B3: Tạo server ảo Ngrok giúp kết nối giữa localhost và internet

## B1: Cấu hình đăng ký slack (Sau khi làm theo xong có thể thử bỏ 1 số bước)
### 1.1 tạo tài khoản slack (đăng ký bằng google cho nhanh)
### 1.2 tạo tài khoản tạo workspace và channel
![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701938302/slack_bot/create_workspace_1.png)
![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701938362/slack_bot/create_channel_2.webp)

### 1.3 tạo ứng dụng
![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701938532/slack_bot/create_app_3.1.png)
![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701938532/slack_bot/create_app_3.2.png)
![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701938532/slack_bot/create_app_3.3.png)

- Chọn workspace mình muốn

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701938532/slack_bot/create_app_3.4.png)
![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701938532/slack_bot/done_create_app_3.5.png)

### 1.4 phân quyên cho ứng dụng
- Mặc định thì ứng dụng của bạn ta sẽ không thể làm gì cả, không thể nhắn tin, vvv. Ta cấp quyền trong OAuth & Permissions

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701938532/slack_bot/Set_Permission_4.1.png)

- Vì chưa rõ phần cấp quyền nên tạm thời cứ cấp thế này

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701939322/slack_bot/Set_Permission_4.2.png)
![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701939322/slack_bot/Set_Permission_4.3.png)

### 1.5 Sau khi cấp quyền xong thì install app
- Cấp quyền lấy token

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701939587/slack_bot/install_app_5.1.png)
![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701939587/slack_bot/install_app_5.2.png)
![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701939587/slack_bot/install_app_5.3.png)

### 1.6 Tạo  (Phần quan trọng)
- Tạo câu lệnh slack trong này

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701939587/slack_bot/slack_command_6.1.png)

- Trong này có các thành phần
  - Command: tên lệnh mỗi khi gọi boot
  - Request URL: Khi boot nhập lệnh nhắn tin xong thì nó sẽ gửi thông tin qua server này. Vì không có tiền ta sẽ tạo server ảo thông qua Ngrok **Chi tiết sẽ có trong B3**
  - Short Description: Mô tả câu lệnh sau khi tạo xong
  - Usage Hint: Mô tả câu lệnh sau khi nhập
  
![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701939587/slack_bot/slack_command_6.2.png)

# B2: Tạo laravel và code
- Ở đây ta viết thẳng vào trong api.php luôn
- Đoạn này bao gồm test gửi message, Lấy tất cả thông tin của tin nhắn trong channel này

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701940712/slack_bot/Channel_ID.png)

```sh
Route::get('/bach/event', function (Request $request) {
//    $response = Http::withHeaders([
//        'Content-Type' => 'application/json',
//        'Authorization' => 'Bearer xoxp-6314543714097-6287373635079-6304522049988-5fa6233ae1694c78d2c0cd08188fb0a4',
//    ])->post("https://slack.com/api/chat.postMessage", [
//        'channel' => "C068VPUB2LT",
//        'text' => "Bách gửi thử tin nhắn slack 2",
//    ]);

    $response = Http::withHeaders([
        'Content-Type' => 'application/json',
        'Authorization' => 'Bearer xoxp-6314543714097-6287373635079-6304522049988-5fa6233ae1694c78d2c0cd08188fb0a4',
    ])->get("https://slack.com/api/conversations.history", [
        'channel' => "C068VPUB2LT",

    ]);

    $responseData = $response->json();

    return response()->json($responseData);
});
```

- Đoạn này là đoạn lấy thông tin slack command trả về mỗi khi nhập lệnh slack

```sh
Route::post('/bach/slack', function (Request $request){
    Log::info($request->all());
    $input = 'aaaa';
    Log::info($input);
    return response()->json([
        'response_type' => 'in_channel',
        'text' => "test slack bot ok! information",
    ]);
});
```
- Thông tin xem Log trong storage/logs/laravel.log

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701941093/slack_bot/laravel_log_7.1.png)

- Để slack có thể truyền dữ liệu vào localhost ta cần có một server ảo như đã nói. Mục đích là để kết nối giữa localhost với internet. Chi tiết sang B3

# B3: Tạo server ảo Ngrok giúp kết nối giữa localhost và internet
- Vào link Ngrok. Tạo tài khoản như bình thường (Đăng nhập và tạo bằng google cho nhanh)
- Tải về và chạy bởi vì nó chỉ có 1 file

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701941451/slack_bot/Ngrok_setup_8.1.png)

- Nhập cấu hình key để đăng nhập

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701941451/slack_bot/Ngrok_setup_8.2.png)

- Sau khi nhập xong thì chỉ cần chạy lệnh ngrok http 8000. Vì mặc định port của laravel là 8000 **(Nhớ chạy php artisan serve thì mới có chạy localhost:8000)**

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701941451/slack_bot/Ngrok_setup_8.3.png)

- Quay về đề điền lại thông tin Slack Command

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701939587/slack_bot/slack_command_6.2.png)


- Ta hoàn toàn có thể chạy thử. **(Nhớ chạy php artisan serve thì mới có chạy localhost:8000 rồi mới gán lệnh ngrok http 8000)**

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701941451/slack_bot/Ngrok_setup_8.4.png)
