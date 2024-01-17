### 1. Tải docker
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
