# 1. monolithic và microservice
|  | Monolithic | Microservice |
|---|---|---|
| Cấu trúc | Các thành phần trong dự án được viết thành một khối | Các thành phần trong dự án được tách ra |
| Lỗi xảy ra | 1 thành phần trong dự án bị lỗi thì cả chương trình lỗi | 1 thành phần phần bị lỗi thì chương trình vẫn chạy |
| Khả năng mở rộng | khả năng mở rộng kém vì các thành phần viết chung | khả năng mở rộng cao vì các thành phần được tách ra giúp việc phát triển các luồng dễ dàng |

# 2. Degin parten Saga
 - Trong microservice, mỗi một service đều đảm nhận 1 databse riêng dẫn đến việc dữ liệu ở các service có thể ko được đúng. 
 Từ đó Sage sinh ra để kiểm tra và đảm tính đồng nhất của dữ liệu trong các service trong bài toán transaction
 - Cấu trúc mỗi một transaction sẽ chia ra làm nhiều service, trong quá trình chạy nếu một service bị lỗi thì tất cả service sẽ rollback lại.
 Các cấu trúc này chia làm 2 phần là implimentation gồm Choreography và Orchestration **(Xem chi tiết câu 3)**

# 3. Choreography và Orchestration trong Saga
## Choreography
 - 1 thằng gọi đến từng phần. Nếu phần nào bị lỗi thì rollback hết
![](https://images.viblo.asia/3cdd6152-72bd-4dd7-aaad-e38c1869b754.png)

 - 1 thằng gọi đến tất cả sau đó tất cả báo lại về trả về true mới ok còn ko thì rollback
## Orchestration
![](https://images.viblo.asia/fad9847b-431a-4fa3-8a0a-0ea1c5557a30.png)

# 4. Một số cách xử lý lỗi trong Queue
 - Tạo order backup trong database: Nếu lỗi thì sẽ tự động lưu trong các hàng cần gửi trong database. Phía bên service sẽ dùng craw job hoặc thread dùng sleep để mỗi lần gọi lại lên Queue để xem nó hết lỗi chưa

# 5. API Gateway:
 - Là một API viết chung, dùng để gọi đến các service

***VD: Mình có API của Product, Order, Payment. Tương ứng với địa chỉ localhost: 8091,8092,8093***
**Thay vì gọi đến các địa chỉ localhost: 8091,8092,8093 thì ta gọi thông qua 1 API chung được gọi là API Gateway có 8760**
- **VD gọi tìm đến tất cả Product: http://localhost:8760/api/v1/app1/api/v1/product**
- **VD gọi tìm đến tất cả Order: http://localhost:8760/api/v1/app1/api/v1/order**
- **VD gọi tìm đến tất cả Payment: http://localhost:8760/api/v1/app1/api/v1/payment**
 
![](https://genk.mediacdn.vn/139269124445442048/2022/3/4/photo-1-16463882949582105196548-1646389517721-1646389518274932690753.jpg)
