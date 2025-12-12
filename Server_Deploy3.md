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

# 167 endcodeBase64
```
LS0tLS1CRUdJTiBSU0EgUFJJVkFURSBLRVktLS0tLQpNSUlKS0FJQkFBS0NBZ0VBcVdmV290NEpKZmszQ2p5SVJhOStHUU1URkNmTlBYOU5wRXdUQkJiMzhmNnlvVkJMCndKMExHS3BPQ2dPbThCaXRzRnQ4Ri9LajY5Ukoyd0krN0d1VTZaYTVXcm5yZnl4VEw5RlhtSnM2M214V3dyTTAKa3FZTlhtajlsaFlxdXNwbHZ2LzhpaS90alBmQ0FVSGQyQVd1MjZxNXVTdVBiMC8xc0ZSa3RZamFlMi9rdWRZYgpiYkpBeW80VUw3UmhHQndUNTNObWg3dUtNTm13UUF1OEM5MEVOUU4yc0JQN3lOYUFvYTVpTWN1a0hsUEZ2WTcwCkpUcFZMbWFhNm9vdVZEOGtic0RJZ29vSE5ibkpBVVB4aHlVTVhXQWVWSy8rU0hxZkgrUEtRSndmZzQrUHhxRGkKN2RibHpsT3BKTE03VW9mam81RVBHN1BDaldubVc0amxKaEN4MDBMTUV4QWdtK1k3K3ZoMGJTTUhQdDEvSTBVagpBaVZ6SFRVWURBdlBibTkvQmVUSmdKWm1xWFhCWE1iT21Vb2xqL2dIbTE4WnB6aFlTY0I0b0JDYVhmbkdtNHhJClVSdlhDYk9CK0crenBqRWNCS3ZuUE5UMnI4Rkh4UlpNV3pnTEdjamZ5d21LcGR0dEIvdldpU2h5VjVrN3ZxU28Kb3FVQ0ZMMzRBbFJlMGxVRmNWWkRkcGtxWFpmSzI5b3BCdDZWY2ZmN080VVRZdTFsYk5KdVJtb3ovYWdra2hoVQpkTkRQdkpNWjlqbXBQd0RhaU8yRXFDckZxN25yK2xtcjNYa0I1NlFCdkhSRVg4YTcwSDZEd1lQN0lsWmIrbzZ4CnMxM0F1SlloUVp1QkplUTd0bTZWcng1TERzSWVFV0VMRG5mYUREazVwTVdLUkExaXRRcDhZZUFIUlRjQ0F3RUEKQVFLQ0FnQWdpekF5alpFWVdHMzRhM1NLWHBKTTM4aFVnT2p1dlh2KzZoWmxITHg1SXNMU05vaTI4ZlJsd3FISApUcmhOTzVCeVpzREtJUFRZb3ltbEJ5TnJhNmRwMEdpL1F5UTRoQjFlL0VwbHFMeUFhak9vcDZDYjQ0YUI4bzEwCnZjRnJyT0lxOVNaZ3JhQm5DbG1jd0RpTC9WdUFHNlllS240ZGxqRE90UWU3MEJTWXpnQVVxMHNOb2NiTW9zckIKOTFjSHVLMGlNNHNvM0NCS0RpZkx4ZlZVR2h0cXk4V0xRZXVHdzU1bWNRZXdKVHpjRHAvWU1KUTZhcUJlajV1SApIeENUWXFYdkdOM3NKZlFJb0M0N0xnQkNSQjNCK21zWlBjNE53bkM3UVpsakhCcjV2U1NUdGVpaVpEdzFqT0RiCmlnc0ZhZEdUWkpTUWI5SWFOSlBxVmJ3ZnVlbFBLYjNkSVQxbWVuMndHZFN2bEFnUVFrd3FnOXkvQnJIRTBpNlcKVDFlcFpLeEUyOVpzZ0Zab0xYZlVEeTZSUnJ3anFmL2dTZFMrQXJFQ1UwSm81MUg0MXBJb0V1QmtlYXNiaHF4WgpEbmNNcW5JTUFHT1hsdUhIakI5cFpMcGN2UmhtTmdzSzR4azlWcTBoSkZtRlNINXJ0QnJpOWQzNm9GRk44U2dECjR0N1ZmTkRzMVRReTErc3RqdVVBdFJQdFM1WXVaUys2ODM5TURlaFJ6QWVLaUd1WXQ3RFZGaXdCcGxMT2lYc1YKYXBJR3RMNS9xME4ydDE2S0E2Q2VpOTdva3lDWWdVd1dUc0lKeCt1S1lmTHQ4ZE0zdUdZN2U1L3Q0dzlQbEFhOApGaWxtUlgvbGYwRDVHcmxHa1RVaFNhelh5T1IxZloxbXJ0TlhyNWh3VzRCODhrZFZRUUtDQVFFQTdVbFhnMVZZCnllT1EzdWR1cU5iN2c0UmMyNHJrNDc3QXcxSnRZL1ZUeWFUdTFjTkpIY2FMYmllNWQzYkN5Ryt2Yk9TUzYxbi8KNjMybUpHTUdLZHB3MFFna2IwVmlaUDc4Ukx5VGpSWVY0SWhoYnpZL1hrRFQreHhKT1Izc0ZkbUpWWWZsdkN5YQpCSnlJK2lnQmdnOXB5K1lFRVVUZTcxVExPeVJYME5wUWZaRU1veTlQVWxkS043SXA3Y0sybUVxQ1VwcWhBSFUvCmNjUkthMm9ZL2x5UHpiZFJNOS9WNkdYWDkxazkvSTlNczVaNE5FTDNtd3h6RUdUNnQ4M05EalBMK0hGM0VBdTcKWURJd0N6clJRMU94VDgvNmxqc3ZER1lpdTRvMTAwbTdMdnRwWmQyM01zMkNnVWE2MmxVMm1vQWFwMlFCcjdZUgpiYzFrUXRwN25OTHJ4d0tDQVFFQXRzUUd3d2lEUHI4V1MyU0t6aUlHRHdWME9UY2EzbUVMTzZmc05aNU84R2JaClNIWUJBSmtjc0xHNDl3cTVQWkJxSGloNkFEdWNRQkJXL0x4QWhUWkR4TzB0eFBVZWFtWHFnUWlBSFo4V0NleGQKUjllcVA3MjlQQ3Fqd1hPSjNPb0xkYmViZlFiWXpiSUtRdnJVT2RvS0E3SG1VWDFmOG05aTZ5NEI0N2kzY3JhdwpJbkg0d0VHZXFMZDN4SWhzL3RuaHRjT0EzMndxOFBKYVVBMkUrbi9aZVI2TDhaR2V2UTJhQk5nMUF6NUc2aUtyClRmUVkyeGhRVTc5UnNGQzhqNHRoZFE2Mm9lZ0hZcVc0dlREeWJ1amlYM0pDaTdDdVRwQnFiMDI0aEtOV3VOMzgKNzl5RlhkYSsxVjBwNWQ1d3FCenZYMFJlSmxiWjNsU0luZmpXT1Z0N0VRS0NBUUVBblhuOU1GWWw5T2FvTUtiYgpWQVpKS1lGZ3R2czQ2TVNoM1g4SXhqdjhmV2lPY1NPSGxORTltNytWWU9sYVgvZHZMdytMU2RLUys5Q0p3TUJQClNOdUYzOVJOaWVNOFo5YXB5VngxZUQ3ZUNnTzQxanZrVmtNajdCVmJxeUptbWlHaStUYVZpd3IydEhUR20yNk4KZ2FtRkJ5TUNOQXZIQUlMLzFhSksvWHJGekcvRk9VK2Vqd0VMYW1jOVdHUFBGc2JzTXJJWWc5dE1YYzV0clZmZQplb0VubHRsQWRQTHFYYStwWXFqQmNLb1J0MlgzSklnRkY4dHRXY1lLZG8ySXR4STlIZ2IvZzVDbHJEUGltckZRClRDUnhHb3ptdTJsUDBpUytqRVF2Y0tnUUtDQUdWT3FPT0pNWE40Q2ZaV01FT0Frb3AwckJxOEZqVThIcDlreFYKbVVDSjVRS0NBUUE0WGJTSUtmUHdRaGFxSWRQOVJ0ai9nUHNiT2pkN0pnckUxMEV1T0NpNFU3L25iUjFhQmQ2bgpUK2h2cUVzQkJhejBxQjhZTzBveEo5anNFVk1Fd251Y0hGbmxTSU9jNU5teCtlRXBRWXNXZkdNNGFQY0V1WXZICkpvOWlkak9xZ2pRT2xoWEtOWFpmMmV6NFEwdDRuQnBDa1hjcTRyUFluU213eG51bXM2MUFINytxbitQTHgzRWIKTDVvc2JyYk8wbnVlQnpHVHRsUjRBd1ovY2V2MUpjRDRiY2RUTlVuem5HSkg1RFpWVGJ1cE1oQUs5cUZEMFBmVgpIRWdoVElVYThDMmFZSE5LODdoellCRGRxRjdjZmM1ekNWWWtwdFRiUGdiVlZPNzNXVGpCd3hUakZPdTh5U0lKCnc3WE1ReElUaHZqOE5LV2t4VnhrQ1VZcEVqbGZieXRCQW9JQkFDcm15enQ5NUYzaHBzVFFibk4rb1Jxa1hlUDcKemtOUlBGMjlzRGxMeTdVU2E3R1JXSWV0YlZyN1Y2S1VDTHcxdVJHTVRVZjBhL2FKUFVoaFFxeE5MSDczdy9LdgpkcjV6NjhlR29HaFcxcis5MUJEb0xIaEZCMjhRN1lpOTBnV2ZLNU1FNVlrK0p5c3piaHZhTmZOTVpVOVNCOUlwClZSRlQ4L0VuUnVMM2wrdHkyd1RZejA3cUQvNzYvWEdnaEc1blErZ1c5S2FwOW4vRU5iMFlhMWp0UVpjUDduYTcKMDgzbko2eFJxc2JRbjRkbmt0WDhyZXQ5b3Y2M2xSSUVLb0ZLOWJyUjlFaTdaekJqbWlpWnJTVDMycjN5N2wzWAo5UElWQ014eDljR09FN0VSRWpxTnI1VTdyanhKRjFkK1EvSzBnUi9IVXllbGcwYzh1WGI3d2prOHVmND0KLS0tLS1FTkQgUlNBIFBSSVZBVEUgS0VZLS0tLS0K
```

# Lệnh đổi base64 trên server
Khi login vào đc thì
`base64 -w 0 tênvàĐịnhDạngFilePem`

Ví  dụ
`base64 -w 0 deploy.pem`

# Chạy pm2
- `pm2 start ecosystem.config.js`
<img width="1637" height="276" alt="image" src="https://github.com/user-attachments/assets/3cb6b3fa-aea3-4ea5-b24d-0fe630c735c2" />

- `pm2 save` lưu pm2 này
<img width="1815" height="495" alt="image" src="https://github.com/user-attachments/assets/4250ec1d-9430-44ab-8efb-80ca725aaf2b" />

- `pm2 startup`: khởi động lại khi reboot
<img width="1815" height="193" alt="image" src="https://github.com/user-attachments/assets/3b2b7dd5-4bb9-448c-b68a-0a5e92b448d7" />

# Gia hạn toàn bộ ssl
- `sudo certbot renew --post-hook "systemctl reload httpd"`

# build server 167
- Tạo cấu hình VD: `awa-stage.vw-dev.conf`
```
<VirtualHost *:80>
        ServerName awa-stage.d-dxlab.com
        DocumentRoot /var/www/awa/stage/public
        <Directory /var/www/awa/stage/public>
                AllowOverride All
        </Directory>
        <ifModule mod_rewrite.c>
              #RewriteEngine On
              RewriteCond %{HTTPS} off
              RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [R,L]
        </ifModule>
RewriteEngine on
RewriteCond %{SERVER_NAME} =awa-stage.d-dxlab.com
RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]
</VirtualHost>
```
<img width="830" height="455" alt="image" src="https://github.com/user-attachments/assets/aee24891-d7c7-4ae9-b969-5d5ab2c5f6a1" />

- Dừng dịch vụ apache `sudo systemctl stop httpd`
<img width="878" height="162" alt="image" src="https://github.com/user-attachments/assets/e59a1f18-3a7b-4d92-a813-d0b577e537d7" />

- Đăng ký ssl `sudo certbot certonly`
<img width="1896" height="737" alt="image" src="https://github.com/user-attachments/assets/9e02de1b-a0f1-4288-baa5-42a782e26cca" />

- Chọn 2
<img width="1002" height="678" alt="image" src="https://github.com/user-attachments/assets/bc523853-8b85-4549-be6c-471038cd612f" />

- Nhập tên domain ví dụ `awa-stage.d-dxlab.com`. Sau khi enter nếu có 2 file pem hiện lên là thành công
<img width="1538" height="698" alt="image" src="https://github.com/user-attachments/assets/607ce22d-4fa5-4584-a0e8-99a6abfde9f6" />
<img width="1452" height="757" alt="image" src="https://github.com/user-attachments/assets/6c9a681c-2f80-44ee-9583-08b282db5844" />

- Khởi chạy lại `sudo systemctl restart httpd`
<img width="992" height="748" alt="image" src="https://github.com/user-attachments/assets/d3ad219b-bc93-4d69-906d-2a26ff98f5f6" />

- Thêm ngoài (có thể skip). Sau khi có 2 file pem kia thì thêm thông tin cấu hình ssl `awa-stage.vw-dev.conf`
```
<VirtualHost *:80>
        ServerName awa-stage.d-dxlab.com
        DocumentRoot /var/www/awa/stage/public
        <Directory /var/www/awa/stage/public>
                AllowOverride All
        </Directory>
        <ifModule mod_rewrite.c>
              #RewriteEngine On
              RewriteCond %{HTTPS} off
              RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [R,L]
        </ifModule>
RewriteEngine on
RewriteCond %{SERVER_NAME} =awa-stage.d-dxlab.com
RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]
</VirtualHost>


```
