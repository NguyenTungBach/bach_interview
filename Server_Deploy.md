# Cấu hình đăng ký server trên amazon
- ssh -i key.pem deploy@........ **tên địa chỉ**
- passphrase file key.pem: ...... **mật khẩu**

# ***new-web: là tên để thay đổi***

## B1: clone code mới từ trên github (các câu lệnh ở phía dưới)
- cd /var/www/
- git clone https://github.com/VehoWorks/new-web.git new-web
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
