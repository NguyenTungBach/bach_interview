# Khái niệm
## Docker là gì
- Là công cụ được tạo ra để giải quyết vấn đề cài đặt hay triển khai môi trường chạy dự án độc lập trên hệ điều hành

**VD: Để chạy PHP thì mình cần cài composer để quản lý các thư viện, xampp để giả lập môi trường chạy server. Điều này rất tốn thời gian. 
Thay vì cài đặt các môi trường để chạy, thì Docker sẽ giúp ta đóng gói khởi tạo môi trường chạy cần có sẵn đề chạy ứng dụng.**

# Thành phần & File cấu hình
## Phân biệt Docker Image và Docker Container
- Image là một bản thiết kế được build từ dự án. Chỉ đọc
- Container là các tiến trình chạy từ image. Ngoài ra thì muốn chạy container thì cần hệ điều hành linux vì thế nếu chạy trên Window sẽ cần cài máy ảo linux để chạy container

## Docker khác gì so với Máy ảo (VM)
- Docker thì nó được build sẵn các môi trường
- Máy ảo là một hệ điều hành riêng nên rất nặng và chậm

## Docker Compose là gì
- Docker Compose dùng để quản lý nhiều container cùng lúc và chạy các lệnh docker.

## Docker Hub là gì?
- Là kho lưu trữ các Docker Image trên mạng, cho phép người dùng có thể tải về để sử dụng

# Lưu trữ & Mạng
## Docker Volume để làm gì?
- Để gán các cấu hình hay dữ liệu trong container. Đảm bảo sau khi container mất đi thì những dữ liệu gán đó không bị mất

## Các loại Network cơ bản trong Docker?
- Bridge: định, cô lập cho các container trên cùng máy chủ
- Host: dùng chung mạng với máy chủ
- None: tắt hoàn toàn mạng của container

## Lệnh thông dụng
