# 1. In-memory Database (IMDB) là gì?
- Là một loại cơ sở dữ liệu, sử dụng bộ nhớ của máy tính để lưu trữ

# 2. Redis là gì?
- Là In-memory Database và cụ thể hơn là 1 no sql database **(Không có những khái niệm như bảng, table)**. Tất cả dữ liệu đều được lưu dưới dạng key value pair **(cặp khóa có giá trị)** **(giống như JSON cũng có 1 key value thì ta có thể nhìn Redis như là 1 JSON to)**
- Khác với các database lưu trên disk thì REDIS lưu trên RAM. **Mặc dù xử lý nhanh nhưng Điều này dẫn đến 1 vấn đề đó là khi ta khởi động máy tính thì tất cả bộ nhớ trên RAM cũng mất luôn. Nếu đang sử dụng server mà đùng cái mất điện thì xác định mất toàn bộ dữ liệu Redis nếu không Back Up**
- Chính vì nhưng điều này mà Redis không dùng để lưu dữ liệu. Mà nó dùng để lưu những dữ liệu ít bị thay đổi, dữ liệu tính toán, bộ nhớ đệm để sau có thể sử dụng sau này. Đó là lý do Redis Cache thường được dùng

# 3. Ưu và nhược điểm của redis
- Cùng nằm trong Spring Framework

|  | Ưu | Nhược |
|---|---|---|
| Lưu trữ | Lưu trên RAM nên truy vấn nhanh | Lưu trên RAM khi khởi động lại máy, hay sever thì dữ liệu sẽ mất hết nếu không Back up |
| Single Thread | Sử dụng IO mutilplexing | ??? |
