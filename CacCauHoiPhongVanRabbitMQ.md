# 1. Cấu trúc message queue
- Producer gửi
- Broker: trung gian, phân phối message
- Exchange: quyết định message vào queue nào( bộ định tuyến) bằng binding và routing key
- Binding: vận chuyển đến queue. Là liên kết giữa Exchange và Queue thông qua routing key
- Routing key: Là địa chỉ của queue, quyết định tin nhắn đến queue nào
- Queue: hàng đợi
- Consumer: nhận

![](https://jstobigdata.com/wp-content/uploads/2020/03/direct-exchange-rmq-min.png)

# 2. Bất đồng bộ trong queue
- Phía bên gửi có thể gửi mà không phải chờ bên nhận xác nhận

# 3. Ưu nhược điểm message queue
- Ưu:
  - Đảm bảo tính toàn vẹn dữ liệu ***(Khi dữ liệu gửi từ producer sẽ được gửi y nguyên đến consumer )***
  - Khả năng chịu lỗi cao ***(Nếu có lỗi xảy ra tin nhắn sẽ chờ đến khi hết lỗi sẽ gửi tiếp )***
  - Tăng hiểu suất xử lý dữ liệu nhờ bất đồng bộ ***(Phía bên gửi có thể gửi mà không phải chờ bên nhận xác nhận )***
  - Phát triên mở rộng ***(Dễ dàng giúp có các service giao tiếp với nhau với nhiều loại service code khác nhau )***

- Nhược:
  - Chi phí cao vì tốn nhiều chi phí để giao tiếp với các service
  - Phức tạp khi có nhiều service với nhau vì cần biêt nhiều thông tin để giao tiếp
  - Giảm sát ***(Cần đảm bảo tổn thất dữ liệu khi queue đầy vì khi đó queue sẽ không nhận thêm message nào cho đến khi xử lý xong )***
  
# 4. Các kiểu RabbitMQ
- direct exchange: Đúng với các routing key sẽ nhận


- topic exchange: các routing key macth với điều đầu hoặc cuối sẽ nhận
Ví dụ: Đăng ký kênh trong YouTube. Kênh sau khi ra video sẽ báo tất cả ai đăng ký kênh

- fanout: gọi đến tất cả queue trong exchange đó, không cần routing key
Ví dụ: Viettel đầu tháng có chương trình khuyến mại sẽ gửi thông báo cho tất cả thuê bao

- Header: Các key dưới dụng header
Routingkey sẽ chứa nhiều thông và consumer phải có đầy đủ các thông tin đó thì mới được nhận

- Dead letter:
Nếu consumer không được nhận thì tin nhắn sẽ lưu trữ ở một nơi và quay lại về exchange để gửi lại

# 5. Một số đặc điểm của các message queue:
- Kafka chuyên xử lý loại dữ liệu nặng
- ActiveMQ hỗ trợ chia vùng dữ liệu nhưng config phức tạp
- ZeroMq Gửi tin nhắn nhẹ và nhanh và không có tính bảo mật
- AWS SQS hỗ trợ trên nền tảng cloud mới dùng được nên chi phí cao

# 6. Vì sao RabbitMQ được sử dụng?
- Giả sử nếu các service giao tiếp nhau thông qua API:
  - Nếu có một service chết thì các service gửi message đến nó sẽ bị mất hết. Vậy nên cần một message broker như RabbitMQ để tránh trường hợp mất message
  - Tại một thời điểm serive nhận nhiều request sẽ xảy trường hợp quá tải. RabbitMQ sẽ tạo hàng đợi để xử lý từng request

# 7. So sánh RabbitMQ và Kafka?
- RabbitMQ thường dùng cho các số lượng tin nhắn ở mức trung bình. Theo kiểu point to point(producer gửi đến consumer duy nhất)
- Kafka (kiểu pub-sub) thường dùng cho các số lượng tin nhắn lớn và yêu cầu độ trễ thấp
