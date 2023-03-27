# 1. monolithic và microservice
|  | Monolithic | Microservice |
|---|---|---|
| Cấu trúc | Các thành phần trong dự án được viết thành một khối | Các thành phần trong dự án được tách ra |
| Lỗi xảy ra | 1 thành phần trong dự án bị lỗi thì cả chương trình lỗi | 1 thành phần phần bị lỗi thì chương trình vẫn chạy |
| Khả năng mở rộng, phát triển | khả năng mở rộng kém vì các thành phần viết chung | khả năng mở rộng cao vì các thành phần được tách ra giúp việc phát triển các luồng dễ dàng và phát triển tính năng nào thì chỉ phát triển ở thành phần đó mà thôi |
| Chi phí và tài nguyên | Ít tốn tài nguyên, chi phí hơn Microservice |  tốn tài nguyên, chi phí |
| Giao tiếp giữa các service trong hệ thống | Không có | phức tạp, việc giao tiếp giữa các service có thể khác nhau(cái thì json, cái thì xml), Đồng bộ hóa realtime giữa các service phức tạp |
| Auto-scale | Không có | Xảy ra khi quá nhiều request gửi vào một service và service đó không kham nổi thì hệ thống sẽ tự động tạo thêm một service nữa để xử lý. Khi không cần nữa thì có thể giảm |
| Đặc điểm | Có thể nắm bắt được toàn bộ nghiệp vụ vì tất cả viết trên 1 project | Không thể nắm được toàn bộ nghiệp vụ vì mỗi modul riêng lẻ |

# 2. Nếu bị hỏi về nghiệp vụ microservice
- Chỉ nói là làm ở từng service nhỏ

# 3. Các cách giao tiếp giữa các microservice
- Call api: restfull webservice (body truyền đi là json) và soap(xml)
- File: ví dụ gọi vào file để đọc ra các giao dịch cần đối soát trong ngày. Không lo cơ chế authen mà chỉ cần authen File server
- Message queue: giao tiếp thông qua một thằng thứ 3 như rabbitMQ, redit, kapca  
