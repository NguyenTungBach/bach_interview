//////////////////////////
## 1. Câu lệnh kiểm tra dung lượng các ổ đĩa trên server
- `df -h`

<img width="524" alt="image" src="https://github.com/user-attachments/assets/e878b2db-ee03-4eed-8451-c27f695b914a">

## 2. Câu lệnh kiểm tra dung lượng của các folder trong 1 folder
- `du -hs * | sort -hr`

## 3. Câu lệnh kiểm tra docker nào đang chạy trên trên server
- `sudo docker ps`

![image](https://github.com/user-attachments/assets/2af509ca-a43f-47dd-b174-32ca6d4e6351)

## 4. Câu lệnh kiểm tra toàn bộ docker đang tồn tại trên server
- `docker images`

![image](https://github.com/user-attachments/assets/240dc9e8-1b9b-4265-a74b-20468f1b1dfa)

## 5. Câu lệnh xóa docker trong CONTAINER (khu vực lưu trữ docker được chạy)
- `docker rm ID_contant`

![image](https://github.com/user-attachments/assets/e2d193b6-12ee-4e08-bfae-1009508c77ff)

## 6. Câu lệnh xóa docker trong IMAGES (khu vực lưu trữ docker)
- `docker rmi ID_images`

![image](https://github.com/user-attachments/assets/6b942642-bdac-4a6e-8245-ab49333e9380)


## 7. Build docker trên server
- `sudo docker ps` câu lệnh trên để kiểm tra xem có những docker nào đang chạy
- `docker stop ID_contant`: dừng chạy docker
- `docker rm ID_contant`: xóa docker trong CONTAINER
- `docker build -t TênDocker .`: Build lại docker hoặc tạo. Lưu ý **bắt buộc phải vào project**
- `docker run -d -p port:port TênDocker`: Chạy docker. Lưu ý port phải không tồn tại trong `docker ps` và tên docker là ở `docker build -t TênDocker .`

## 8. Xử lý vấn đề docker làm đầy bộ nhớ
- Kiểm tra toàn bộ dung lượng docker `sudo docker system df`

![image](https://github.com/user-attachments/assets/c00a4a45-2c67-45a7-bed9-df8b09e6f495)

- Cách xử lý là xóa đi những container, image, volume, build cache không dùng
  - Xóa container đã dừng `docker container prune -f`
  - Xóa image không sử dụng: `docker image prune -a -f`
  - Xóa volume không dùng: `docker volume prune -f`
  - Xóa mọi thứ không còn sử dụng (container, image, volume, build cache): `docker system prune -a -f`
  - Xóa mọi thứ không còn sử dụng (container, image, volume): `docker system prune -a --volumes`

  - Xóa mọi thứ không còn sử dụng: container dừng, image không dùng, network, volume rác, build cache: `sudo docker system prune -a --volumes -f`
    - Lệnh này:
        - Xóa mọi thứ không còn sử dụng: container dừng, image không dùng, network, volume rác, build cache.
        - Không cần xác nhận thủ công (-f).
        - Yêu cầu quyền sudo (tùy hệ thống, có thể không cần nếu user đã trong nhóm docker).
        ![image](https://github.com/user-attachments/assets/cee892dd-aa6f-451a-aac7-3aeb11799f7f)
        ![image](https://github.com/user-attachments/assets/cb630875-3e35-4a82-8e27-e52a1e72657c)



- VD dùng lệnh xóa mọi thứ không còn sử dụng (container, image, volume, build cache): `docker system prune -a -f`

![image](https://github.com/user-attachments/assets/06fadb58-89e3-4f16-a1d6-94e2b03423ca)

![image](https://github.com/user-attachments/assets/38552afe-1148-4195-bf2d-5ef31900bb8a)

- Kiểm tra lại bộ nhớ sau khi clear

![image](https://github.com/user-attachments/assets/3f047259-f2bd-4062-bb52-b95d4ce7339a)
![image](https://github.com/user-attachments/assets/b0ad8fb6-74bf-4850-9146-3f4e18f7da8b)

## 9. Xử lý vấn đề log pm2 làm đầy bộ nhớ
- `sudo du -sh /home/*`: kiểm tra dung lượng home

![image](https://github.com/user-attachments/assets/765c7928-92f5-4a5a-90de-088c07b8e70e)

- `sudo du -sh /home/ec2-user/*`: kiểm tra dung lượng ec2-user

- `pm2 flush`: lệnh xóa toàn bộ log pm2 *(Không xóa đi file mà chỉ xóa nội dung log)*

![image](https://github.com/user-attachments/assets/a29afb4f-04de-4851-b2ec-9b3030f81083)

## 10. Build docker với nextjs không bị bộ nhớ cao trên server
- Yêu cầu cần có:
  - docker-compose.yml (chứa cấu hình docker)
  - CustomDockerfile (khai báo trong docker-compose.yml, dùng để cập nhật build docker)
  - file deploy ci/cd (vì không có tên rõ ràng chỉ biết đuôi yml)

### 10.1 docker-compose.yml
```
version: '3.3'
services:
  ai_chat_1on1_admin_web: # tên build phải khác nhau
    build:
      context: .                   # Thư mục gốc chứa Dockerfile
      dockerfile: CustomDockerfile  # Tên Dockerfile tùy chỉnh
    ports:
      - "3005:3005"                # Liên kết cổng (cấm được trùng port trên server `docker ps` và phải giống port trong, thay đổi nếu cần)
    restart: always
```

### 10.2 CustomDockerfile (Ví dụ)
```
FROM node:20-alpine AS runner


WORKDIR /app

# Set NODE_ENV to production
ENV NODE_ENV production

# Disable Next.js telemetry
# Learn more here: https://nextjs.org/telemetry
ENV NEXT_TELEMETRY_DISABLED 1

# Set correct permissions for nextjs user and don't run as root
RUN addgroup nodejs
RUN adduser -SDH nextjs
RUN mkdir .next
RUN chown nextjs:nodejs .next

# Copy các file và thư mục đã build từ server gốc vào Docker image
COPY --chown=nextjs:nodejs ./.next/standalone ./
COPY --chown=nextjs:nodejs ./public ./public
COPY --chown=nextjs:nodejs ./.next/static ./.next/static

USER nextjs

# Exposed port (for orchestrators and dynamic reverse proxies)
EXPOSE 3005
ENV PORT 3005
ENV HOSTNAME "0.0.0.0"
# HEALTHCHECK --interval=30s --timeout=30s --start-period=5s --retries=3 CMD [ "wget", "-q0", "http://localhost:3005/health" ]

# Run the nextjs app
CMD ["node", "server.js"]
```

### 10.3 ci/cd ( .yml) (mở `npm run build` và đoạn deploy quy định đẩy lên)
```

      - uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Install dependencies
        run: npm install

      - name: Build
        run: npm run build

      - name: Deploy
        run: |
          #rsync -rzu --delete --exclude='.next/**' --exclude='.next' --exclude=.env ./ deploy@${{ env.deploy_host }}:${{ env.deploy_path }}
          # ssh deploy@${{ env.deploy_host }} "cd ${{ env.deploy_path }}"
          if [ "${{ github.ref }}" == "refs/heads/develop" ]; then
          export HOST="18.180.33.240"
          export USER="deploy"
          export DEPLOYPATH="/var/www/aichat/aichat-fe-admin"
          fi
          rsync -rzu --delete --exclude=.env ./ $USER@$HOST:$DEPLOYPATH
          ssh $USER@$HOST "cd $DEPLOYPATH && docker-compose up -d --build"
        env:
          DEPLOY_USER: deploy
```
### 12. Trên server đảm bảo kiểm tra chính sách khởi động lại (restart policy), nếu `always` (khởi động lại nếu docker chết) thì đúng, nếu là `no` thì là sai
`sudo docker inspect --format '{{.HostConfig.RestartPolicy.Name}}'`

![image](https://github.com/user-attachments/assets/5a94304d-10bb-4046-b7c8-0a5dadfb82ba)

//////////////////////////
## 13. Hướng dẫn build giọng nói aivis
***
Các bước
  1. Setup image aivis cho docker
  2. Tải giọng hoặc chọn
  3. Tìm giọng nói sau khi đã build
***

### 13.1 Setup image aivis cho docker
- Trên server tạo 1 folder để làm nơi chứa file docker-compose.yml và danh sách giọng nói đã tải về
- `docker-compose.yml`: Với image đã được build lấy ở trên mạng cụ thể `ghcr.io/aivis-project/aivisspeech-engine:cpu-ubuntu20.04-1.1.0-dev`
```
aivis-engine:
  container_name: aivis-engine
  image: ghcr.io/aivis-project/aivisspeech-engine:cpu-ubuntu20.04-1.1.0-dev
  ports:
    - "10101:10101"
  volumes:
    - ./models:/root/.local/share/AivisSpeech-Engine/Models
  restart: unless-stopped
```
- Sau khi build xong thì sẽ thế này

<img width="1918" height="1033" alt="image" src="https://github.com/user-attachments/assets/7c7a0e69-8f32-454c-a272-95e79e86205c" />

