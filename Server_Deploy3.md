# 1. Một số câu lệnh trên GIT
`git cherry-pick <commit-hash>`: muốn merge một commit cụ thể từ nhánh khác

![image](https://github.com/user-attachments/assets/d1eaa6dd-2bb7-468f-af49-5c57658d198d)

![image](https://github.com/user-attachments/assets/b4d91552-6013-4771-b229-edb2ffc32579)


# 2. Kiểm tra lỗi khi cấu hình của Apache `(httpd.service)` không hợp lệ, khiến dịch vụ không thể reload.

## 2.1 Mô tả lỗi
- Khi chạy lệnh `sudo service httpd reload`
```
[deploy@ip-172-31-23-55 conf.d]$ sudo service httpd reload
Redirecting to /bin/systemctl reload httpd.service
Job for httpd.service invalid.
```
## 2.2 Các bước kiểm tra
### 2.2.1 Kiểm tra các file .conf cấu hình lỗi
- Lệnh `sudo apachectl configtest` để kiểm tra cấu hình lỗi 
  - Nếu file không lỗi cuối dòng sẽ có từ `Syntax OK`
 ![image](https://github.com/user-attachments/assets/0f69f8dc-2cd8-4388-a404-36feed4c7dcd)

 - Nếu file có lỗi thì vị trí và tên file sẽ được báo
 ![image](https://github.com/user-attachments/assets/a20c0705-dc19-4ef0-950c-68d9c8abadd1)

### 2.2.2 Kiểm tra trạng thái dịch vụ
- Lệnh `sudo systemctl status httpd` kiểm tra trạng thái dịch vụ
  - Ví dụ trong hình là báo lỗi ngày 4/6/2025 về việc `Apache (httpd) đã dừng (inactive/failed) nên không thể thực hiện reload`
  ![image](https://github.com/user-attachments/assets/c7ad9633-fa52-419d-aa41-4168cf664887)

## 3. Lệnh chạy docker migrate:fresh
- `docker exec -it tênImages npm run migrate:fresh`
- Ví dụ `docker exec -it aichat_workspace_develop npm run migrate:fresh`

# 4. Xử lý trường hợp server từ reboot thủ công sang reboot hệ thống:
## 4.0 Kiểm tra xem người dùng có chủ động reboot không
- `last -x | egrep "shutdown|reboot"`

![image](https://github.com/user-attachments/assets/5ce3d85c-a41c-49c7-ba91-3d57c0224662)

- Lần reboot gần nhất: Nov 26 — không có dòng shutdown đi kèm. Thì khả năng reboot bằng lệnh reboot
- Dòng shutdown ngay trước dòng reboot (ví dụ: Nov 5 và Nov 4) → chứng tỏ các lần đó là shutdown chủ động (thủ công), sau đó là khởi động lại (reboot)

## 4.1 Kiểm tra Apache đang chạy
- Lệnh `ps aux | grep httpd`

- Như này là đang chạy bình thường

![image](https://github.com/user-attachments/assets/a95d3b28-48ec-4f93-8eff-f87efaa7b2c6)

## 4.2 Tắt toàn bộ Apache
- `sudo pkill -9 httpd`: (buộc dừng toàn bộ các tiến trình (process) có tên là httpd)

![image](https://github.com/user-attachments/assets/976568f3-d0ca-4850-9947-1982c4290c7c)

## 4.3 Khởi động lại dịch vụ Apache
- `sudo systemctl start httpd`: Khởi động lại dịch vụ Apache
- `sudo status httpd`: Kiểm tra lại trạng thái dịch vụ

![image](https://github.com/user-attachments/assets/9208864b-c506-47d5-9bb7-cb1731ed932b)

# 3. Larvel setup .env thư nhưng cấu hình vẫn nhận thư cũ
`php artisan queue:restart`: dành cho trường hợp chạy queue nếu setup email .env nhưng vẫn sử dụng mail cũ (lệnh này buộc các queue worker hiện tại khởi động lại) 

Khi nào nên chạy queue:restart?
| Trường hợp                               | Có nên chạy `queue:restart`? |
| ---------------------------------------- | ---------------------------- |
| Bạn vừa cập nhật code                    | ✅ Nên chạy                   |
| Bạn thay đổi nội dung job, hoặc mailable | ✅ Nên chạy                   |
| Bạn update `.env` (như đổi MAIL\_\*)     | ✅ Nên chạy                   |
| Gặp lỗi kỳ lạ trong queue                | ✅ Nên chạy                   |
| Muốn kill tất cả job đang chạy           | ✅ Nên chạy                   |

VD: đã cập nhật mail trong env
- Lúc trước:
  - `MAIL_FROM_ADDRESS=driveelink-stage.help@driveelink.co.jp`
- Sau đó:
  - `MAIL_FROM_ADDRESS=driveelink-stage.help@driveelink.co.jp`
  - Kể cả có chạy `php artisan config:clear` thì cũng sẽ không cập nhật dược cấu hình queue

<img width="1530" height="607" alt="image" src="https://github.com/user-attachments/assets/bf8078ed-d233-47fe-ad8b-67cb78746343" />

- Để khắc phục cần chạy `php artisan queue:restart`
<img width="737" height="102" alt="image" src="https://github.com/user-attachments/assets/c4ef216e-96a3-4b50-8456-39f0f0829c43" />

- Sau khi khắc phục

<img width="1537" height="720" alt="image" src="https://github.com/user-attachments/assets/257aa753-f0de-445a-9b00-6795e2e36e91" />

