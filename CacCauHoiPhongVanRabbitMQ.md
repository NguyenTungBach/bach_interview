# 1. Cấu trúc message queue
- Producer gửi
- Broker: trung gian, phân phối message
- Exchange: quyết định message vào queue nào( bộ định tuyến) bằng binding và routing key
- Binding: vận chuyển đến queue
- Routing key: đảm bảo tin tính toàn vẹn của tin nhắn
- Queue: hàng đợi
- Consumer: nhận

# 2. Bất đồng bộ trong queue
- Phía bên gửi có thể gửi mà không phải chờ bên nhận xác nhận

# 3. Ưu nhược điểm message queue
- Ưu:
  - Đảm bảo tính toàn vẹn dữ liệu ***(Khi dữ liệu gửi từ producer sẽ được gửi y nguyên đến consumer )***
  - Khả năng chịu lỗi cao ***(Nếu có lỗi xảy ra tin nhắn sẽ chờ đến khi hết lỗi sẽ gửi tiếp )***
  - Tăng hiểu suất xử lý dữ liệu nhờ bất đồng bộ ***(Phía bên gửi có thể gửi mà không phải chờ bên nhận xác nhận )***
  - Phát triên mở rộng ***(Dễ dàng giúp có các service giao tiếp với nhau với nhiều loại service code khác nhau )***
