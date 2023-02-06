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

# 5. Oauth2
- Là một phương phương thức giúp các ứng dụng bên thứ 3 truy cập vào tài nguyên của người dùng trên một ứng dụng khác ***(VD: một ứng dụng nào đó muốn được truy cập vào tài nguyên ảnh google của người dùng)***.
- Gồm 4 thành phần chính: 
  - Resource owner: Người dùng
  - Resource server:  Tài nguyên của người dùng ***(cụ thể VD ở đây là tài nguyên ảnh google của người dùng)***
  - Client: Những ứng dụng bên thứ 3
  - Authorization server: Xác thực, kiểm tra thông tin user gửi bằng cách sinh ra các ***access token***. Có thể tự dùng làm Resource server.

- Mô tả quá trình VD của google:
  - Người dùng(Resource owner) đăng nhập vào web của ứng dụng.
  - Ứng dụng(Client) chuyển hướng người dùng đến ***Authorization server(tức là ứng dụng của google để xin truy cập tài nguyên)***
  - Người dùng sau khi đăng nhập vào Authorization server và nhấn đồng ý. Phía Authorization server sẽ gửi về 1 đoạn mã authorization code cho Client dùng để xác minh lại thông tin người dùng gửi. Trong đó có Client ID, Client sercret (Ứng dụng phải này đã đăng ký với Authorization server trước đó).
  - Nếu thông tin hợp lệ Authorization sẽ trả về access token cùng với refresh token (nếu có).
  - Ứng dụng từ đó lần sau chỉ cần gửi access token cho Authorization server là được phép truy cập tài nguyên
