<img width="350" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/28ab9dc6-042f-400e-b1d5-2ee674dfc7f9">### 1. Tải docker
### 2. Tạo file docker
- Tạo folder (tên tự đặt)
  - tạo folder data (yêu cầu vị trí đặt như mình đã để trong vd đoạn **volumes** file docker dưới đây)
  - Tạo một file docker đuôi **.yml** VD tạo file docker cho mysql:
    - ```sh
      version: '3.3'

      services:
        mysql:
          container_name: mysql-hosei
          image: mysql:8.0.16
          command: ["--default-authentication-plugin=mysql_native_password", "--sql_mode=NO_ENGINE_SUBSTITUTION"]
          environment:
            MYSQL_ROOT_PASSWORD: rootpass
            MYSQL_USER: khong
            MYSQL_PASSWORD: khongpass  
          volumes:
            - ./data:/var/lib/mysql
          ports:
            - 3308:3306
          restart: unless-stopped
          networks:
            - app-network
        #   restart: unless-stopped
      
      #Docker Networks
      networks:
        app-network:
          driver: bridge
      ```

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1705476930/docker/docker_sql.png)

### 3. Chạy CMD trong thư mục này

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1705477313/docker/image_pk0wdh.png)

### 4. Chạy Navicat để kết nối môi trường database
- theo như cấu hình ở trên
  -  Connection name: (tự đặt)
  -  Host: localhost
  -  Port: 3308
  -  User Name: khong
  -  Password: khongpass
 
![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1705477823/docker/download_e8pcrv.png)
