//////////////////////////
## Câu lệnh kiểm tra dung lượng các ổ đĩa trên server
- `df -h`

<img width="524" alt="image" src="https://github.com/user-attachments/assets/e878b2db-ee03-4eed-8451-c27f695b914a">

## Câu lệnh kiểm tra dung lượng của các folder trong 1 folder
- `du -hs * | sort -hr`

## Câu lệnh kiểm tra docker nào đang chạy trên trên server
- `sudo docker ps`

![image](https://github.com/user-attachments/assets/2af509ca-a43f-47dd-b174-32ca6d4e6351)

## Câu lệnh kiểm tra toàn bộ docker đang tồn tại trên server
- `docker images`

![image](https://github.com/user-attachments/assets/240dc9e8-1b9b-4265-a74b-20468f1b1dfa)

## Câu lệnh xóa docker trong CONTAINER (khu vực lưu trữ docker được chạy)
- `docker rm ID_contant`

![image](https://github.com/user-attachments/assets/e2d193b6-12ee-4e08-bfae-1009508c77ff)

## Câu lệnh xóa docker trong IMAGES (khu vực lưu trữ docker)
- `docker rmi ID_images`

![image](https://github.com/user-attachments/assets/6b942642-bdac-4a6e-8245-ab49333e9380)


## Build docker trên server
- `sudo docker ps` câu lệnh trên để kiểm tra xem có những docker nào đang chạy
- `docker stop ID_contant`: dừng chạy docker
- `docker rm ID_contant`: xóa docker trong CONTAINER
- `docker build -t TênDocker .`: Build lại docker hoặc tạo. Lưu ý **bắt buộc phải vào project**
- `docker run -d -p port:port TênDocker`: Chạy docker. Lưu ý port phải không tồn tại trong `docker ps` và tên docker là ở `docker build -t TênDocker .`

## Xử lý vấn đề docker làm đầy bộ nhớ
- Kiểm tra toàn bộ dung lượng docker `sudo docker system df`

![image](https://github.com/user-attachments/assets/c00a4a45-2c67-45a7-bed9-df8b09e6f495)

- Cách xử lý là xóa đi những container, image, volume, build cache không dùng
  - Xóa container đã dừng `docker container prune -f`
  - Xóa image không sử dụng: `docker image prune -a -f`
  - Xóa volume không dùng: `docker volume prune -f`
  - Xóa mọi thứ không còn sử dụng (container, image, volume, build cache): `docker system prune -a -f`

- VD dùng lệnh xóa mọi thứ không còn sử dụng (container, image, volume, build cache): `docker system prune -a -f`

![image](https://github.com/user-attachments/assets/06fadb58-89e3-4f16-a1d6-94e2b03423ca)

![image](https://github.com/user-attachments/assets/38552afe-1148-4195-bf2d-5ef31900bb8a)

- Kiểm tra lại bộ nhớ sau khi clear

![image](https://github.com/user-attachments/assets/3f047259-f2bd-4062-bb52-b95d4ce7339a)
![image](https://github.com/user-attachments/assets/b0ad8fb6-74bf-4850-9146-3f4e18f7da8b)

## Xử lý vấn đề log pm2 làm đầy bộ nhớ
- `sudo du -sh /home/*`: kiểm tra dung lượng home

![image](https://github.com/user-attachments/assets/765c7928-92f5-4a5a-90de-088c07b8e70e)

- `sudo du -sh /home/ec2-user/*`: kiểm tra dung lượng ec2-user

- `pm2 flush`: lệnh xóa toàn bộ log pm2 *(Không xóa đi file mà chỉ xóa nội dung log)*

![image](https://github.com/user-attachments/assets/a29afb4f-04de-4851-b2ec-9b3030f81083)

