# 1. In-memory Database (IMDB) là gì?
- Là một loại cơ sở dữ liệu, sử dụng bộ nhớ của máy tính để lưu trữ

# 2. Redis là gì?
- Là In-memory Database và cụ thể hơn là 1 no sql database **(Không có những khái niệm như bảng, table)**. Tất cả dữ liệu đều được lưu dưới dạng key value pair **(cặp khóa có giá trị)** **(giống như JSON cũng có 1 key value thì ta có thể nhìn Redis như là 1 JSON to)**
- Khác với các database lưu trên disk thì REDIS lưu trên RAM. **Mặc dù xử lý nhanh nhưng Điều này dẫn đến 1 vấn đề đó là khi ta khởi động máy tính thì tất cả bộ nhớ trên RAM cũng mất luôn. Nếu đang sử dụng server mà đùng cái mất điện thì xác định mất toàn bộ dữ liệu Redis nếu không Back Up**
- Chính vì nhưng điều này mà Redis không dùng để lưu dữ liệu. Mà nó dùng để lưu những dữ liệu dùng đi dùng lại (tài khoản, user id), dùng cho web (VD thông tin người dùng), bộ nhớ đệm để sau có thể sử dụng sau này. Đó là lý do Redis Cache thường được dùng
- Caching là một kỹ thuật tăng độ truy xuất dữ liệu và giảm tải cho hệ thống. Lưu ý phải update cache
- Rabitt MQ là 1 message queue
- Thường để lưu dữ liệu dụng JSON

# 3. Ưu và nhược điểm của redis
- Cùng nằm trong Spring Framework

|  | Ưu | Nhược |
|---|---|---|
| Lưu trữ | Lưu trên RAM nên truy vấn nhanh | Lưu trên RAM khi khởi động lại máy, hay sever thì dữ liệu sẽ mất hết nếu không Back up |
| Single Thread | Sử dụng IO mutilplexing | ??? |
| Tính nhất quán dữ liệu | ??? | vấn đề xảy ra khi cả hay cùng update dữ liệu |

# 4. Đồng bộ và bất đồng bộ
- Đa luồng giúp giải quyết nhiều công việc cùng 1 lúc
- Bất đồng bộ (bài toán nấu cơm, trong lúc nấu cơm có thể làm nhiều việc). Trong lúc chờ công việc này có thể làm nhiều việc khác.( trong lúc chạy vì biết xử lý dòng 5 mất thời gian, thay vì đợi thì làm việc khác giúp tránh mất thời gian)

- Đồng bộ là chạy theo từng dòng. Dòng trên chưa xong thì dòng dưới nó ko đc chạy tiếp. (asyn, synchronization).

- Khác nhau giữa đa luồng và bất đồng bộ là số người làm công việc. 
- Bất đồng bộ là 1 mình tôi làm nhưng nhiều công việc

- Đa luồng là nhiều người làm nhiều công việc. Vấn đề là về xung đột tài nguyên như thằng rửa rau và rang thịt đều cần dùng chung cái bếp.

# 5. Thread và Process
- Thread là 1 đơn vị xử lý nhỏ nhất của máy tính, hoạt động của cpu
- Process là 1 app dựng lên

# 6. Khi nào dùng thread
- 
