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
  - Kể cả có chạy `php artisan config:clear` thì cũng sẽ không cập nhật được cấu hình queue

<img width="1530" height="607" alt="image" src="https://github.com/user-attachments/assets/bf8078ed-d233-47fe-ad8b-67cb78746343" />

- Để khắc phục cần chạy `php artisan queue:restart`
<img width="737" height="102" alt="image" src="https://github.com/user-attachments/assets/c4ef216e-96a3-4b50-8456-39f0f0829c43" />

- Sau khi khắc phục

<img width="1537" height="720" alt="image" src="https://github.com/user-attachments/assets/257aa753-f0de-445a-9b00-6795e2e36e91" />

# Các lệnh điều tra khi server nặng
- `sudo du -sh /home/*`: Thống kê dung lượng toàn bộ trong folder cụ thể ở đây là folder `home`

<img width="622" height="853" alt="image" src="https://github.com/user-attachments/assets/480c44b1-4477-4161-a2cc-51895f6f606c" />

- `sudo du -sh /home/* | sort -hr` thêm sắp xếp nhưng sẽ lâu nếu nhiều file

<img width="796" height="808" alt="image" src="https://github.com/user-attachments/assets/da263f6c-12e4-4e9a-aaf2-18efef6ad5ad" />


- Giả sử Sau khi chi tiết tìm được file nào trên server nặng thống kê 10 file nặng `sudo du -ah /home/deploy | sort -rh | head -n 10`

<img width="880" height="308" alt="image" src="https://github.com/user-attachments/assets/9a799a9c-5e7a-4fed-b8d3-46d28fcad51f" />

# 240 encodeBase64
```
LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUFNd0FBQUF0emMyZ3RaVwpReU5UVXhPUUFBQUNBVUw0K1ZOQ3ppMFE3ZzM4elAxWGFJaGp4dnhaSFYveTl1NUI0bFVWbmdZUUFBQUpEcFdnMmI2Vm9OCm13QUFBQXR6YzJndFpXUXlOVFV4T1FBQUFDQVVMNCtWTkN6aTBRN2czOHpQMVhhSWhqeHZ4WkhWL3k5dTVCNGxVVm5nWVEKQUFBRUM0eHRiRG9RZU5VV0I1VG44b25iYjZsMFBlS014eVY4R3lJZitmeHA2US9oUXZqNVUwTE9MUkR1RGZ6TS9WZG9pRwpQRy9Ga2RYL0wyN2tIaVZSV2VCaEFBQUFDV2h2WVVCc2IyTmhiQUVDQXdRPQotLS0tLUVORCBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0K
```

# 142 endcodeBase64
```
LS0tLS1CRUdJTiBSU0EgUFJJVkFURSBLRVktLS0tLQ0KTUlJRW9nSUJBQUtDQVFFQTBWN0pvaEFvY1c0bTZkMUNIMmZ2VnJvaHdUaGNCbHFmbFlCUXhjWThXYWhoalEwNw0KT3RQM0pDVDRYeUdFL2t2amhoRXBJUFBGUVJ3MUVrYVg2RUZQeFFmbG1rd3M5dFhSMmxaTDExa1FoK2FEbjQ1MA0KQTRlOE5xTU5JemE5WHpZc2hQVDY5M1ZKQ0JNOFVycUZ2R0UzNUN1R3l0NzJjbFdSUG5SK1FSd09LWmdqa3lyRg0KazJXTVhPNm9pR24vYkhkdmdzSkROQy9TVm5UaHBIVllBRjRwZUw2bVNWMGQ1UDVtUWViYkZad1JMaUIrTUd2bQ0KSXpFdXMrUjUzMVhTQkN5aVZCMWluQkg5NE03OGhjblpsVlhhVmJWWWw5ZGxYOGZjcC9YYmhaMHhwRGNqRnBCZg0KTm5BbGdlY1NSL0FLbEZPSkc0cDAxQjR0K3RKalM1amg1N3c4b3dJREFRQUJBb0lCQUdndHhDTFI2MjNWbzZORw0KcHpvOVcwaEtRYldGTjdVcHJyS1RNSjNZYi9zazM3VngyZ0VCcTczZWIzL1dpL2lGQm1lVmJtT3BLSU9uWjNqNg0KaTJmVDU3OWdtSXpZVHA5YjhabTB5dlFTcXprVUtIWmlTYlBmL0hVcldNUW0zci9ia3ZkdGR0dGZEc0huNEdKQg0KMFgzVTJoeTgwOHRxZWpLV0JUbVFlYW9vTFp2ZjQ0QnZoTUFEZXZsNzllQlFtUjg2V2h3ZnVvclVKblJhZnorWg0KY1IwdlVrd3dONWNjK2xzdkFvWkIyb3RsSWtwK1pVL0NwbWlwR2hkOWFWUXZpdWY4TTBwNzVBNGVTdHpPREJUMw0KN013aVlXQXhybDlMRGVvL2FyaVg1TGgxMThSRmYyWUQva3BxQVoxOHc3dzU4bkMyZTZCUWVKRTVDcTVDQ20yZw0KOHI1VHFHRUNnWUVBN3ZMSjhjd1g0L0QxeC80TStLSnR6Slo4TlMya1JTWEFuSzExMGVucjNTQnN2R0kxSGJiKw0KZkYyK1NJdHJtSTJobUNaV253cml3U3Y0UXhuNWhrWXJKYUhlUkdrdEdqOHF5VGlGQTl2NjU2cjJqd1M0aVVXKw0KSzNCaHpGWUYxd09Idjg2RUxrenRYU3BOSklSdEVKa0dJVTVrUitlT2Y5S29walNaNzZRNlQza0NnWUVBNEUrbg0KSkRPQ3hBQVYxWkJEWER2Ykx1Z2RQbEVLSHR1Qk1yaEl1d2FKeW1EZmNRdFBmZno0cVlZcnpPdkJqRldSQ05DeQ0KaE5ucVpJdWx6amtkYi9lcWNyU0xsNFNoRmZtVzhTbVl5ZEtMcjg4UmdvMkJFdXNaRmtoUGUra1hNL3pDZzR6YQ0KVnNOckt5S1BzckNjUitJa2dLSTArVzJid1VFakg0MHlHS2habWZzQ2dZQVlGOExrN244NkxJR2J1TEgySCtxUw0KUmxvZndvcGRyb0ROUzNBbHlrQk4rNGI3TjZ2RFkwQWxxZzRWb25rbTJLRUNobHNWampOdTV0QVJjLzBFM081Yw0KelFWc1FHNmJ4dUs1aDBsaUtqd1NQOXE4Y08xcWFlM1MwM0lJK0dOK1dvekZlajA1cmVnQkROTGFhNy9UZkpweA0Kb1VYYk9pM1VGWm1McUtJYzE2SkpnUUtCZ0ZENkVHSE9RcmZWUEF5a0R0MCtNb3RGZWtFajZsNW5hY1hRcDFqMQ0KTEVzbUc2UG9yR0xVTDBTcnppWWxPZk1hZE1oVTV3MTB5ZHhRV2FRUUZHTjJhazhNaEpSSGFndlAxY0RyL2w5bA0KcGMzckYrd2tmMk5BQWdkOFJVMTdRVWdnU0d4TExndENjdTdZaEQzQzZqZzlHR1pqcUhJZk1xcGFoSDZBYjRSZA0KU2pOL0FvR0FadnFIRWpnMzlEeEp6S0VRNjBwNTlDVGRwSFJ5MGFwODFyUmF0K1lWRHdMc29sUnJrdGtVbUcrcQ0KMENtTTNXcVlmOWFMTXI5bDg3Ym1rYlViTWM2UE1HTkROTHE4TWhrMGh5SHA1eW0zcDhtMWwwTkVEN2NHUnd1TA0KeHZoVS9mdEJHbi9yQ2J3dW8vdXBzL2JYUjVGTnh2V1E5dCtQRlNUUTI3OE4rMzR6UC8wPQ0KLS0tLS1FTkQgUlNBIFBSSVZBVEUgS0VZLS0tLS0NCg==
```
