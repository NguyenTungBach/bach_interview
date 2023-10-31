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
- rmdir <forder> : xóa thư mục
- ls : xem thông tin thư mục
- ls -a : xem thông tin tất cả bao gồm thư mục ẩn
- cd .. : lùi thư mục
- cd <tên> : chạy đến một thư mục
- cd ../ : chạy ra hẳn ngoài
- npm run prod: lệnh load lại code cho project front end
- php artisan config:clear : lệnh clear cache nếu dữ liệu env không nhận
- gặp lỗi này thì ở storage tạo thư mục **framework và bên trong framework có 3 thư mục cache,sessions,views:** Script @php artisan package:discover --ansi handling the post-autoload-dump event returned with error code 1
- Cấp quyền toàn bộ: sudo chmod -R 777 storage

//////////////////////////
## tương tấc với server bằng php storm 2021.2
- vào php storm: **Tools -> Deployment -> Browser** remote host
  - Đặt tên server
  - Type: SFTP
  - SSH config
    - Nhập địa chỉ Host
    - Tên của con server đó
    - Authentication type = Key pair
    - Private key file là đường dẫn ở trong máy
    - Sau khi nhập xong hãy nhấn vào nút Test Connection để kiểm tra kết nối
  - Root path: nhập đường dẫn trên server giúp mình không cần phải click chuột chạy đến mất thời gian

- Sau khi kết nối xong nếu muốn sử dụng terminal luôn thì có thể gọi theo **Tools -> Start SSH Session -> SERVER cấu hình mình muốn chọn**
![](https://res.cloudinary.com/dark-faith/image/upload/v1693204639/veho%20tutorial/cau_hinh_quan_ly_server1.png)
![](https://res.cloudinary.com/dark-faith/image/upload/v1693204639/veho%20tutorial/cau_hinh_quan_ly_server2.png)

//////////////////////////
## Trường hợp đặc biệt về lỗi cấu hình npm sau khi đã lỡ tải node js và nvm
- yêu cầu ban đầu **nên tải node js trước rồi nvm sau** 
- lỗi nvm đổi phiên bản nhưng không được:
  - xóa nodejs -> cho nvm tải một phiên bản nào đó
  - chạy npm -v và node -v kiểm tra xem đã đổi chưa
 - lỗi not found khi chạy nvm install
   - chạy npm config list
   
   ![](https://res.cloudinary.com/dark-faith/image/upload/v1693205263/veho%20tutorial/npm_config_list_right_qysi2a.png)

   - Nếu không đúng dạng như trên thì phải vào C:\Users\USER_NAME/.npmrc kiểm tra xem có đùng như dưới đây không nếu không thì sửa lại cho đúng

    ![](https://res.cloudinary.com/dark-faith/image/upload/v1693205496/veho%20tutorial/file_npmrc_rv44oo.png)

//////////////////////////
## Một số chạy code trong project
- react native:
  - yarn run android: chạy code android
  - ./gradlew assembleRelease: (cd ./android) tự động build lại file android. **Lưu ý chỉ dành cho project không có expo**
  - yarn start: chạy code môi trường android
  - expo prebuild: chạy code generate file android và file ios
  - expo eject: build lại môi trường generate file android và file ios (lưu ý nhớ xóa file android)
  - yarn install: cài file node_module cho project
  - yarn run watch: chạy font end
  - yarn run prod: load lại font end
  - yarn run build: load lại font end (Tùy trường hợp, Yêu cầu đi cùng yarn run generate)
  - yarn run generate: load lại font end (Tùy trường hợp, thường đi cùng yarn run build)
  - yarn run lintfix: sửa lỗi khi yarn install báo lỗi (do bị trùng file), lỗi eslint
  - npx react-native start: run và xoá cache từ cd android
  - pod install: kiểm tra các gói ios đã đủ chưa
  - npm install --legacy-peer-deps: trường hợp chạy yarn install không khớp với các phiên bản đã cài đặt hiện tại
  - npm run test TênFile -- -t 'TênTest': chạy một test và skip các test còn lại trên fornt end
  - php artisan serve --env=testing: chạy database test
  - php artisan migrate:fresh --seed --env=testing: tạo bảng và seed dữ liệu mẫu file test (trước khi chạy nhớ config:clear)
  - php artisan test tests/Feature/TênĐườngDẫnFile --filter=TênHàmTest: chạy unit test back end
  - php artisan dusk tests/Browser/TênFolderHoặcKhông --filter=TênFile: chạy file IT test
  - npm run test TênFile -- -t 'TênTest': chạy một test và skip các test còn lại trên fornt end
  - DB::connection()->getDatabaseName(): kiểm tra xem đang chạy db nào (Dùng để check UT và IT)

## Trường hợp git yêu cầu đăng nhập lại
- lệnh: git remote set-url origin https://nguyentungbach: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@github.com/VehoWorks/v-face.git

//////////////////////////
## chạy unit test
- test file: php artisan test tests/Feature/tên_file.php
- test hàm trong file: php artisan test tests/Feature/tên_file.php --filter=tên_hàm
