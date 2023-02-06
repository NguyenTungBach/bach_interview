# 1. Rest API là gì?
Là 1 giao thức tạo ra API. 
 - get -> lấy
 - post -> gửi
 - put sửa
 - delete -> xóa

# 2. RestFull API là gì?
Là giao thức định nghĩa ra các chuẩn giao thức viết API
 - get/products -> lấy tất cả product
 - get/products/{id} -> lấy product theo id
 - put/products/{id} -> sửa product
 - delete/products/{id} -> xóa product

# 3. JWT là gì?
- Dùng để tạo ra token thông qua thuật toán mã hóa
- Cấu trúc gồm 3 phần: header, payload, signature
- Header: chứa kiểu dữ liệu và thuật toán sử dụng để mã hóa JWT
  - VD: { "typ": "JWT", "alg": "HS256" }
- Payload: chứa các thông tin mình muốn đặt trong chuỗi token như username, password,...
- Signature: chữ ký mã hóa. Phần chử ký này sẽ được tạo ra bằng cách mã hóa phần header , payload kèm theo một chuỗi secret (khóa bí mật). Dùng để định danh đảm bảo dữ liệu gửi đi không bị thay đổi

# 4. SOAP
- Là 1 giao thức dựa trên XML dùng để truy cập vào các Webserice
- SOAP chậm bởi vì sử dụng định dạng XML để phân tích cú pháp
- VD: https://www.youtube.com/watch?v=WZalO30AppI
