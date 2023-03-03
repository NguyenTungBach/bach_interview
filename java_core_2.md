## 1. Khác nhau giữa interface và abstract class
Điểm chung đều thể hiện tính trừu tượng.

|  | Interface | Abstract class |
|---|---|---|
| Khai báo | Interface phải dùng từ khóa impliment | Abstract class phải dùng từ khóa extend |
| Số lượng kế thừa | Interface được nhiều | Abstract class extend được 1  |
| Access modifile | Access modifile của Interface chỉ là public | Abstract class có thể lựa chọn public, private, default, protect  |
| Chứa bên trong | Interface chỉ chứa hàm | Abstract có chứa thuộc tính, function implementation **(function abtract)** , function chi tiết  |
| Thường sử dụng | Interface thể hiện 100% tính trừu tượng nên hay dùng làm bản phác thảo giúp cho các tính năng ko bị thiếu | Abstract class thường dùng khi muốn các class con kế thừa nó có thể sử dụng chung hàm, ngoài ra cho phép chứa các thuộc tính giới hạn truy cập access modifile |

## 2. Đa hình
1 hành vi của đối tượng thì sẽ thể hiện theo nhiều cách khác nhau

|  | Đa hình tĩnh **(compile time polymorphism)** | Đa hình động **(run time type polymorphism)** |
|---|---|---|
| Xảy ra | tại thời điểm gọi đến hàm, ta biết phải truyền tham số gì. |tại thời điểm chạy chương trình, hàm đó thể hiện chạy theo nhiều cách khác nhau |
| Chi tiết | Cùng kết quả trả về nhưng tham số truyền vào khác nhau về kiểu dữ liệu, số lượng, vị trí | 1 hàm Cùng tham số truyền vào, cùng 1 kết quả trả về nhưng được thể hiện nhiều cách khác nhau |

## 3. @Data

- Sẽ biên dịch gồm @Getter, @Setter, @RequiredArgsConstructor, @ToString và @EqualsAndHashCode

**Vấn đề hàm toString: nó sẽ gọi đến những thuộc tính không mong muốn ví dụ như thuộc tính của mình là
class khác. Nếu chẳng may mà class được gọi đó lại có gọi đến thuộc tính của class mà mình đang
gọi => sẽ dẫn đến vòng lặp vô tận**

## 4. Bean
- Là những class mà mình sử dụng trong project. Khi khai báo Bean sẽ được IOC trong spring
quản lý các Bean đó.

## 5. Các cách khai báo Bean

- @Bean: đặt trên hàm, kết quả của hàm này sẽ được IOC quản lý và trả về kết quả đó
- @Component: chú thích trên class, là một khuôn mẫu chung cho bất kỳ thành phần nào do Spring quản lý
- @Repository: chú thích cho class giúp truy vấn dữ liệu database
- @Service: chú thích cho class xử lý logic
- @Controller: chú thích class làm việc với Request

## 6. Khác nhau giữa String và String Builder

- String Khi tạo ra 1 biến thì nó là không thay đổi, kể cả khi ta có gán cho nó 1 giá trị khác
hay cộng chuỗi vào nó thì bản chất nó sẽ chỉ tạo ra giá trị khác với giá trị được cộng dồn vào.

**Nên khi nối chuỗi sẽ dùng String Builder. Nhưng chi khi nào nối nhiều chuỗi**

## 7. Maven 

- Dùng để lưu trữ các thư viện
- Cách sử dụng: Vào file pom.xml copy thẻ dependency lấy từ trên mạng rồi đưa vào trong dependencies. 
Reload lại nó sẽ tải file jar về. Nếu có rồi thì nó sẽ ko tải nữa

## 8. Dependency in version
- Là 1 nguyên lý thiết kế code 

## 9. Inversion of Control (IoC)

- Là 1 desgin partten
**VD: **

## 10. Dependency injection (DI)

***Lưu ý: Dependency là những thuộc tính từ class khác VD: private Student student; private Teacher teacher;***
- Là một mẫu thiết kế phần mềm mà các đối tượng phụ thuộc sẽ được inject vào một lớp nào đó 
- Mục đích tạo ra nhằm giảm phụ thuộc giữa các Class với nhau

**VD: tính giảm phụ thuộc thể hiện ở @autowire. Trong project làm về Api, mỗi lần gọi sẽ đến api thì các đối tượng trong project đó sẽ bị khởi tạo lại 1 lần. Để tránh việc khởi tạo new đối tượng nhiều lần như vậy thì @autowire sẽ giúp khởi tạo 1 lần trên project, giúp cho mỗi lần gọi đến api các đối tượng đã khởi tạo rồi sẽ không phải khởi tại lại. Từ đó làm giảm tính phụ thuộc giữa các class với nhau**

- Có 3 dạng DI gồm:
  - Constructor Injection: 
  - Setter Injection:
  - Interface Injection:

![](https://toidicodedao.files.wordpress.com/2015/09/ioc-and-mapper-in-c-8-638.jpg?w=474&zoom=5)

## 11. Mối quan hệ giữa Dependency in version, Inversion of Control và Dependency injection (mối liên hệ giữa ba câu 8,9,10)
- Dependency injection
**VD: 

## 12. Vai trò của queue trong microservice
**VD: ta gửi quảng cáo hay tri ân cảm ơn cho 1000 khách hàng. 
Theo thông thường thì ta sẽ dùng vòng lặp for cho mỗi khách hàng để gửi cái mail. Nhưng nếu đã gửi theo cách đó thì xác định cái biểu tượng thực hiện sẽ xoay xoay mãi, chưa kể bị lỗi.**

- Từ đó Queue sinh ra là để giúp admin không phải chờ. Cụ thể ở đây gửi mail là luồng chính sẽ không thực hiện nữa. Chỉ hiểu đơn giản ở đây là tôi gửi 1 danh sách lưu trữ lại.

**VD khác: Khi đi tìm việc, thay vì mình phải đi khắp nơi rồi chờ để phỏng vấn thì mình đi đến nơi trung gian là trung tâm việc làm để đăng tin rồi chờ đợi có người nhận**

### => RabbitMQ là 1 thằng trung gian giúp tránh sự chờ đợi hay phụ thuộc. Dùng để giảm tải xử lý request dồn dập

## 13. Các loại queue trong rabitMQ

- 1 ) Fanout: one for all (1 cho tất cả). Ta gửi 1 thông báo, tất cả đều nhận

- 2 ) Direct : gửi theo khóa định tuyến routing key. Giống mapping, ta gửi và kèm theo key là hello thì tất cả thằng nhận nào có key là hello sẽ nhận được (ĐÂY LÀ CÁI RabbitMQ mà mình hay dùng) 

- 3 ) Topic: cách gửi cũng giống Direct thông qua routing key nhưng khác biệt ở chỗ là gửi đến những cái key có tên giống và  có *. 

**VD: ta gửi thông qua key taxi.any.larger thì queue sẽ gửi đến những thằng key có tên thế này taxi.*.larger**

- 4 ) Header: thay vì gửi thông qua routing key thì nó định tuyến dựa trên giá trị tiêu đề. Ta sẽ gửi thông qua tất cả những thằng header nào có cùng key và value.

**VD: gửi headers {from=New York; to = New York} nhận arguments {x-match= all; from=New York; to New York}**

**VD 2: gửi headers {from=New York; to = Jersey} nhận arguments {x-match= any; from=New York; to = New York}**

- 5 ) Dead Letter: là cái mà không thấy cái hàng đợi nào có cùng routing key hay headers sẽ tự động hủy


## 14. Đồng bộ và bất đồng bộ
- Đa luồng giúp giải quyết nhiều công việc cùng 1 lúc
- Bất đồng bộ (bài toán nấu cơm, trong lúc nấu cơm có thể làm nhiều việc). Trong lúc chờ công việc này có thể làm nhiều việc khác.( trong lúc chạy vì biết xử lý dòng 5 mất thời gian, thay vì đợi thì làm việc khác giúp tránh mất thời gian)

- Đồng bộ là chạy theo từng dòng. Dòng trên chưa xong thì dòng dưới nó ko đc chạy tiếp.

- Khác nhau giữa đa luồng và bất đồng bộ là số người làm công việc. 
- Bất đồng bộ là 1 mình tôi làm nhưng nhiều công việc

- Đa luồng là nhiều người làm nhiều công việc. Vấn đề là về xung đột tài nguyên như thằng rửa rau và rang thịt đều cần dùng chung cái bếp.
