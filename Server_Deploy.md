# Cấu hình đăng ký server trên amazon
- ssh -i key.pem deploy@........ **tên địa chỉ**
- passphrase file key.pem: ...... **mật khẩu**

# ***new-web: là tên để thay đổi***

## B1: clone code mới từ trên github (các câu lệnh ở phía dưới)
- cd /var/www/
- git clone https://github.com/VehoWorks/new-web.git new-web
 - Trường hợp đăng nhập lỗi thì hãy lấy token và làm giống như sau: https://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@github.com/VehoWorks/v-face.git
 - trường hợp muốn xem remote của git này: git remote -v
### cài đặt các bước cần thiết cho web theo file README.md nếu có.

## B2: tạo file config apache mới cho web mới 
- cd /var/www/conf.d/
- cp izumi-cloud.vw-dev.conf new-web.vw-dev.conf
## B3: sử dụng nano hoặc vim sửa nội dung bên trong file new-web.vw-dev.conf
- nano new-web.vw-dev.conf

```sh
<VirtualHost *:80>
        ServerName new-web.vw-dev.com
        DocumentRoot /var/www/new-web/public
        <Directory /var/www/new-web/public>
                AllowOverride All
        </Directory>
        <ifModule mod_rewrite.c>
              #RewriteEngine On
              RewriteCond %{HTTPS} off
              RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [R,L]
        </ifModule>
RewriteEngine on
RewriteCond %{SERVER_NAME} =new-web.vw-dev.com
RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]
</VirtualHost>
```

## B4: Tạo ssl cho new-web.vw-dev.conf để sử dụng https
- sudo certbot
### chọn in index (có số) cần tạo ssl cho new-web.vw-dev.conf và enter để tiếp tục

## B5: reload lại apache để nhận subdomain new-web.vw-dev.conf
- sudo service httpd reload

//////////////////////////
## Một số câu lệnh chạy trên server
- vim tên thư mục: sửa dữ liệu bên trong (ngoài ra nó sẽ tạo nếu thư mục đó không tồn tại)
  - i : sửa dữ liệu
  - :w : lưu file
  - :wq : lưu file và thoát
  - :q : thoát

- mkdir <forder> : thêm thư mục
- ls : xem thông tin thư mục
- ls -a : xem thông tin tất cả bao gồm thư mục ẩn
- cd .. : lùi thư mục
- cd <tên> : chạy đến một thư mục
- cd ../ : chạy ra hẳn ngoài
- npm run prod: lệnh load lại code cho project front end
- php artisan config:clear : lệnh clear cache nếu dữ liệu env không nhận
- gặp lỗi này thì tạo 3 thư mục **framework và bên trong có 3 thư mục cache,sessionsviews** Script @php artisan package:discover --ansi handling the post-autoload-dump event returned with error code 1

//////////////////////////
## Một chạy code trong project
- react native:
  - yarn run android: chạy code android
  - yarn start: chạy code môi trường android
  - expo prebuild: chạy code generate file android và file ios
  - expo eject: build lại môi trường generate file android và file ios (lưu ý nhớ xóa file android)
  - yarn install: cài file node_module cho project
  - npx react-native start: run và xoá cache từ cd android
  - pod install: kiểm tra các gói ios đã đủ chưa
  - npm install --legacy-peer-deps: trường hợp chạy yarn install không khớp với các phiên bản đã cài đặt hiện tại
  
## Trường hợp git yêu cầu đăng nhập lại
- lệnh: git remote set-url origin https://nguyentungbach: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@github.com/VehoWorks/v-face.git

//////////////////////////
## chạy unit test
- test file: php artisan test tests/Feature/tên_file.php
- test hàm trong file: php artisan test tests/Feature/tên_file.php --filter=tên_hàm
