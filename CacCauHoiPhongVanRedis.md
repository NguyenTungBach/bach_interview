# 1. Redis là gì?
- Là In-memory Database và cụ thể hơn là 1 no sql database **(Không có những khái niệm như bảng, table)**. Tất cả dữ liệu đều được lưu dưới dạng key value pair **(cặp khóa có giá trị)** **(giống như JSON cũng có 1 key value thì ta có thể nhìn Redis như là 1 JSON to)**
- Khác với các database lưu trên disk thì REDIS lưu trên RAM. **Mặc dù xử lý nhanh nhưng Điều này dẫn đến 1 vấn đề đó là khi ta khởi động máy tính thì tất cả bộ nhớ trên RAM cũng mất luôn. Nếu đang sử dụng server mà đùng cái mất điện thì xác định mất toàn bộ dữ liệu Redis nếu không Back Up**
- Tóm lại redis là 1 In-memory Database database (sử dụng bộ nhớ máy tính lưu trên Ram)
- Chính vì nhưng điều này mà Redis không dùng để lưu dữ liệu. Mà nó dùng để lưu những dữ liệu dùng đi dùng lại (tài khoản, user id), dùng cho web (VD thông tin người dùng), bộ nhớ đệm để sau có thể sử dụng sau này. Đó là lý do Redis Cache thường được dùng
- Caching là một kỹ thuật tăng độ truy xuất dữ liệu và giảm tải cho hệ thống. Lưu ý phải update cache
- Cache server
- Thường để lưu dữ liệu dụng JSON
- Enqueue (Ghi) và Dequeue (Đọc) ***(Kiểu list)*** 

# 2. Redis một số kiểu dữ liệu
- String:
  - Key
  - Value: Dạng String


- Hash:
  - Key
  - Value: Key-Value

- List:
  - Key
  - Value: Danh sách liên kết
***Thường dùng để làm queue vào trước ra trước và có thể xử lý theo kiểu ***
