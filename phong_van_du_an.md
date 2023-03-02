# 1. Đa luồng (nếu không trả lời được)
Em nói thật là phần này em chưa được làm nhiều. Hồi trước em học có làm với bài liên quan đến mutil thread về chat server nhưng trên 
thực tế ở ngoài em chưa đc có cơ hội làm nhiều với thread.

# 2. Khi bị hỏi mình build cả hệ thống trong micro service
Em thực tế chỉ build phần order thôi. Hồi trước em tham gia dự án ấy thì công ty có phát triển dự án theo đúng mô hình của micro service. Mà em
học được ở trên trang **microservice.io**. Em thì không tham gia hết tất cả các module, em chỉ tham gia module phụ thôi, đó là về thông tin sản phẩm.
Nhưng em cũng có trao đổi với các bạn đồng nghiệp để hiểu luồng của nó như thế nào

# 3. Hỏi về dự án thật có còn đang chạy không, bao lâu rồi
Dự án này của em mới làm được khoảng 6 tháng gần đây. Em là Dev thôi, em không phải là người chịu trách nghiệm chính cho sản phẩm đó và em chỉ chịu 1 phần nhỏ thôi.
Công ty em thì có 1 cái rule là private thông tin của khách hàng. Thêm nữa đấy là sản phẩm của khách hàng nên là thực tế sau khi phát triển sản phẩm xong
thì em không quan tâm nhiều.

# 4. Bị hỏi thêm (câu 3) về số lượng sản phẩm đó bao nhiêu người dùng 1 ngày không
Em cũng có phương pháp để theo dõi thông tin về lượt view của người dùng. Nhưng em chỉ tracking trong thời gian em Dev thôi còn sau khi bàn giao sản phẩm.
Tất cả những thông tin đó phải bàn hết cho khách, em không giữ nó nữa và giờ cũng không biết thông tin sản phẩm hiện tại nó thế nào. Em cũng không quan tâm 
đến sản phẩm này còn sống hay đã chết như thế nào, em chỉ quan tâm là làm chức năng có ổn ko

# 5. Team em làm mà thường xuyên muộn DeadLine thì mình xử lý thế nào?
- Kiểm tra có khó khăn về kỹ thuật không
- Team member có đủ không. Nếu không thì tăng nhân sự lên. Nhân sự nếu không thể nào mà thêm được thì OT

# 6. Nên OT tại thời điểm nào
- Để đảm bảo tiến độ công việc. Vì thế trong tuần, ngày nào cũng sẽ ngồi thêm 2 tiếng
- **Trong trường hợp gần đến hạn mọi thứ vẫn chưa xong**, thì lập tức OT qua đêm, ngủ tại công ty

# 7. Minh đã làm việc với queue rồi thì trong dự án mình dùng với queue ở điểm gì
-  Tránh phụ thuộc lẫn nhau giữa các service 
-  Giảm tải, cùng 1 thời điểm tránh service phải nhận nhiều request, queue sẽ giúp phân phối message 1 cách phù hợp

# 8. Giải quyết queue chết
- Thức sự là code thì em không có cơ hội được làm việc với queue đâu. Nhưng nếu em là người xử lý vấn đề này thì 
  - 1 là em sẽ lưu lại thông tin đó trong database, dùng 1 cron job cứ được khoảng thời gian thì em lại kéo thông tin trong đó ra và gửi lại lần nữa
  - 2 là em cũng sẽ lưu lại thông tin đó trong database, dùng thread ngủ trong 1 thời gian nhất đích, khi wake up lại thì tiếp tục bắn lên queue

# 9. Saga parten định nghĩa
Nó chỉ là cách giao tiếp giữa các service với nhau thôi
- Choreography: các service sẽ bắn nối tiếp nhau cho đến khi kết thúc không còn tin nhắn nào nữa
- Orchestration: 1 thằng gửi đến tất cả các service đến nhau luôn và tất cả những thằng trả về đều phải trả về true thì mới hoàn thành

# 10. Facade và API Gateway design partten
|  | Facade | API Gateway |
|---|---|---|
| Cấu trúc | Lấy tất cả thông tin trong nội bộ **(giống lễ tân, muốn đến phòng nào thì chỉ phòng đó)**| Lấy tất cả thông tin bên ngoài **(giống môi giới khách sạn)** |
| VD |  Cụ thể là có 50 hàm trong hệ thống thì gọi đến 50 hàm => biết tất cả hàm trong hệ thống có những gì | lấy tất cả thông tin 10 khách sạn trong khu vực, dù những thông tin khách sản bên ngoài không phải của mình => nếu muốn biết thông tin khách sạn thì đến gặp thằng này |
| Hiểu chung | chứa tất cả thông tin của các order service đang dùng  | chứa tất cả thông tin của các order service nhưng gồm cả sở hữu và không sở hứu |

# 11. Các loại database
Có 2 loại database sequence và no sequence

|  | database sequence | database no sequence |
|---|---|---|
| Mô tả | Tập trung và bảo đảm các ràng buộc đó nên sẽ hy sinh về tốc độ | Tập trung vào tốc độ và bỏ qua các ràng buộc |
