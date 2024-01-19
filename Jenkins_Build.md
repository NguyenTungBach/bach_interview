### 1. Tạo Project Laravel và đẩy lên git mới
- Lưu ý trong Project sử dụng file Jenkins build cụ thể Jenkinsfile dưới đây, trong này sẽ thực hiện 2 câu lệnh git clone + composer update và php artisan config:clear
```sh
  pipeline {
    agent any

    stages {
        stage('Run Clone Test') {
            steps {
                script {
                    git 'https://github.com/NguyenTungBach/bach_laravel_jeknkins.git'
                }
            }
        }
        stage('Run Artisan Command config clear') {
            steps {
                script {
                    bat 'composer update && php artisan config:clear'
                }
            }
        }

    }
}
```

### 2. Tạo server ảo Ngrok giúp kết nối giữa localhost và internet
- Vào link Ngrok. Tạo tài khoản như bình thường (Đăng nhập và tạo bằng google cho nhanh)
- Tải về và chạy bởi vì nó chỉ có 1 file

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701941451/slack_bot/Ngrok_setup_8.1.png)

- Nhập cấu hình key để đăng nhập

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701941451/slack_bot/Ngrok_setup_8.2.png)

- Sau khi nhập xong thì chỉ cần chạy lệnh ngrok http 8000. Vì mặc định port của laravel là 8000 **(Nhớ chạy php artisan serve thì mới có chạy localhost:8000)**

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701941451/slack_bot/Ngrok_setup_8.3.png)

- Ta hoàn toàn có thể chạy thử. **(Nhớ chạy php artisan serve thì mới có chạy localhost:8000 rồi mới gán lệnh ngrok http 8000)**

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1701941451/slack_bot/Ngrok_setup_8.4.png)

- Ở đây ta chạy với port của Jenkins

### 3. Thêm link server ảo Ngrok của Jenkins vào Webhook Git để mỗi khi đẩy code lên git, git sẽ tự động truyền request vào linkn này

<img width="1124" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/92340d05-90d8-4265-99d5-937d9e2a1a5b">
<img width="1033" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/52c1c931-d29f-49ff-90fc-6343a130d84c">

### 4. Tạo Job quản lý jenkins và chọn Freestyle Project
<img width="1076" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/8e6dc10d-8bf2-4f9d-bb66-cb0bb560fab3">

### 5. Cấu hình để Jenkins kết nối với dự án git
<img width="1156" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/6e366739-41da-4b8a-9782-3d920051a960">
