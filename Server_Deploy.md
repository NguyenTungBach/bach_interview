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
  - ./gradlew clean: (cd ./android) xóa lại cấu hình android **dành cho trường hợp thay đổi đường dẫn file. Nhớ xóa ứng dụng trước khi chạy**
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
  - php artisan config:clear (reset lại cấu hình)
  - php artisan reload:cache (reset lại cache)
  - crontab -l: kiểm tra danh sách schedule
  - crontab -e: xem hoặc thay đổi danh sách schedule
  - sudo ln -s $14 /usr/local/bin/node: fix lỗi xcode không tìm được đường dẫn trên ios (chạy yarn run ios không chạy được)

## Trường hợp file git pull về không đồng bộ
- sudo git clean -d -f(chỉ dành cho server): xóa toàn bộ file sửa. Để sau đó git pull lại

## Trường hợp git yêu cầu đăng nhập lại
- lệnh: git remote set-url origin https://nguyentungbach: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@github.com/VehoWorks/v-face.git

## Trưởng hợp vừa git pull về xong nhưng muốn quay lại 
- git reflog: xem lịch sử vùa pull git
- git reset --hard MÃ: quay lại về lịch sử code 
   
![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1700714718/git_command/git_reset_back_after_git_pull.png)

## Share link local host
- ipconfig lấy địa chỉ ipV4
![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1700735812/share_link_local/download_kdfvp9.png)

- chạy php artisan serve --host=Tênipv4
![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1700735912/share_link_local/download_xr0rbd.png)

- link (nhớ kiểm tra port sử dụng): Tênipv4:8000 
![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1700736017/share_link_local/download_sgugz4.png)

//////////////////////////
## chạy unit test
- test file: php artisan test tests/Feature/tên_file.php
- test hàm trong file: php artisan test tests/Feature/tên_file.php --filter=tên_hàm

//////////////////////////
## cập nhật lên server php 8.2
- php82 -f /usr/local/bin/composer update: Cập nhật lên 8.2

//////////////////////////
## Lưu ý pull code
- git pull --rebase origin TênNhánh: pull code về để check conflic mà không update thêm 1 commit. Mục đích là để cho commit sạch
- git rebase --continue (trong khi đang git rebase): kiểm tra xem nhánh hiện tại tiếp nhận cập nhật nhánh chính ok chưa (Nếu OK thì git add + push lên là được -> Ta sẽ)
  <img width="1280" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/17c1d783-ed41-4dc9-9bb8-86ead2a242db">
- git rebase --about: bỏ pull cập nhật từ nhánh chính
- git log: Kiểm tra chi tiết các commit trên các nhánh
- git log --oneline: Kiểm tra tên các commit trên các nhánh 
  - Các commit nhánh Local: (HEAD -> TênNhánhTrênLocal)
  - Các commit trên git: (origin/TênNhánh)
  <img width="1280" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/4343b867-c8b6-48f4-b46a-830bf6dc6efc">
  <img width="1055" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/81f03fc3-2b84-4105-9f33-4a5f5f55f05a">

//////////////////////////
## Gộp nhiều commit
- git log --oneline: Kiểm tra tên các commit trên các nhánh 
  - Các commit nhánh Local: (HEAD -> TênNhánhTrênLocal)
  - Các commit trên git: (origin/TênNhánh)
  <img width="1280" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/67061a49-0f90-479b-aeee-61206efc4ca0">
  <img width="1280" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/cfafd758-53e4-45fa-8d04-46fe49b5f1f2">

- git rebase -i Head~N: Gộp sửa các nhánh git (cụ thể ở đây là git rebase -i Head~3).
  <img width="1045" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/af27a847-b493-4c43-af73-e6073cad31f4">
- Sửa lại đoạn này (s ở đây là squash, dùng để gộp với phía trước)

```sh
  hint: Waiting for your editor to close the file...
pick 754135b Git Test Multi commit Bach 1
s fa5d4d9 Git Test Multi commit Bach 2
s cd6571c Git Test Multi commit Bach 3

# Rebase d3e2cd5..cd6571c onto d3e2cd5 (3 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
```
- Sau khi lưu xong sẽ có thông báo đã được thay đổi dưới đây
  <img width="1280" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/73a23709-050e-48c9-a831-b59532d8bafc">
  <img width="1280" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/90443932-8b9d-4750-8cbb-8e4f8711e149">
- git commit --amend: Để đổi lại tên git commit
  <img width="1259" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/6268be80-c725-4b96-95a9-26b1b14920b2">
  <img width="745" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/67826a6c-4eb7-4323-af8c-4064e03ae98f">

- Sau khi xong thì thì có thể git push lên như thường (nếu muốn chắc hơn dùng git rebase --continue). (Ở đây là local đã push code lên nhánh bach)
  
  <img width="768" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/eb61adfd-158c-41b1-83f0-94ae5af2660c">

//////////////////////////
## Đổi nhánh nhưng vẫn muốn giữ lại những file những thay đổi
- git stash: lưu file vừa sửa vào bộ nhớ tạm
- git stash apply (sau khi git stash): lấy file thay đổi từ bộ nhớ tạm

//////////////////////////
## Reset commit
- Nếu git add sai và đã nhỡ commit rồi. VD
<img width="1271" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/7f5b2c9f-b025-4a6d-8ef6-4be86b4582a9">
<img width="1266" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/eaecde0e-7af1-48c2-b8d8-f38ef3ef9b1e">

- git reset --soft Mẫ: Quay về commit mình cần mà không làm thay đổi code (cụ thể ở đây là commit trước git reset --soft 706c3bf)
<img width="1154" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/8d3ad1b1-2115-4659-8db0-9b8357290e21">

- Đối với file chỉ vừa mới git add mà chưa git commit thì chỉ cần git reset
<img width="1183" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/ba58c114-3486-4fe8-9caa-ed106a2d2d6a">

//////////////////////////
## htop: Lệnh kiểm tra tiến trình chạy trong hệ thống
- PID (Process ID): ID của tiến trình.
- USER: Tên người dùng chạy tiến trình.
- PR: Độ ưu tiên của tiến trình.
- NI: Ưu tiên của tiến trình.
- VIRT: Tổng lượng bộ nhớ ảo được sử dụng.
- RES: Lượng bộ nhớ vật lý thực sự được sử dụng bởi tiến trình.
- SHR: Lượng bộ nhớ được chia sẻ bởi nhiều tiến trình.
- S: Trạng thái của tiến trình (đang chạy, đang ngủ, đang đợi, v.v.).
- %CPU: Phần trăm CPU sử dụng bởi tiến trình.
- %MEM: Phần trăm bộ nhớ RAM sử dụng bởi tiến trình.
- TIME+: Thời gian CPU đã sử dụng bởi tiến trình.

<img width="1236" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/6b59dc08-65f5-4ce5-a238-cc51b46d58fe">

//////////////////////////
## amazon-linux-extras list: Lệnh liệt kê các phần mềm, các gói môi trường đang chạy trên Amazon Linux
- Tên các phần mở rộng: Đây là danh sách các phần mở rộng có thể được cài đặt hoặc kích hoạt trên hệ thống. Ví dụ, nó có thể bao gồm các gói như "nginx1.12", "php7.2", "python3.8", và nhiều hơn nữa.
- Phiên bản: Đôi khi, lệnh có thể cung cấp thông tin về phiên bản của các phần mở rộng có sẵn để cài đặt.
- Mô tả: Có thể cung cấp mô tả ngắn về mỗi phần mở rộng, giúp người dùng hiểu rõ hơn về chúng và công dụng của chúng.

<img width="852" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/aeb9b5c4-4eab-4832-b460-1f70c0588772">
<img width="721" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/acc6e314-e818-4195-9c7b-8768db104d0f">


