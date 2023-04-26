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
***Thường dùng để lưu info user***

- Hash:
  - Key
  - Value: danh sách nhiều cặp Key-Value khác nhau


- List:
  - Key
  - Value: Danh sách liên kết

***Thường dùng để làm queue vào trước ra trước***

# 3. Redis bài toán thực tế lưu danh sách đơn hàng trong cache, làm sao để lấy ra nhanh nhất
***3 cách dưới đây đều có thể giúp việc dễ quản lý và truy vấn nhanh***

- Cách 1 lưu kiểu String: lưu nhiều key value
  - lưu 1 key xxxxxxxxxx::idkhachhang  -> muốn lấy đơn hàng cụ thể , thì phải parse 1 object to -> lấy dc cái cần tìm

- Cách 2 lưu kiểu String: lưu nhiều 1 key value nhưng trong value là 1 list thông tin json -> phải paser 1 cái object lớn để tìm
  - lưu 1 key xxxxxxxxxx::idkhachhang::iddonhang -> lấy dc luôn , lưu quá nhiều key

***2 cách trên sẽ có nhược điểm chung là nhiều key value đến mức bị quá tải nếu dùng key * với hệ thông dữ liệu lớn có thể query chậm hoặc không load được***

- Cách 3 lưu kiểu Hash: Đây là cách để khắc phục nhược điểm 2 cách trên, thường dùng để lưu value phức tạp nhưng vẫn có thể lấy được value bên trong nó bằng 1 câu lệnh VD hget TÊNKEY TÊNTRƯỜNG
  - lưu key gốc  : xxxxxxxxxx::idkhachhang
  - bên trong lưu nhiều cặp key-value khác nhau ->lưu ít key và không phải 

# 4. Cấu trúc redis
- stand alone: gồm master (cho phép sửa data), slave (đọc data)
- cluster: cũng có master và slave nhưng có thể phân ra thành nhiều vùng

# 5. Caching
- Là một kỹ thuật giúp hệ thống tăng tốc độ truy vấn dữ liệu và giảm tải truy vấn. Bằng cách lưu trữ và dùng lại các dữ liệu đã được truy vấn từ trước, giúp cho hệ thống không phải truy vấn lại.
