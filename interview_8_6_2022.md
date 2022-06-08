## 1. Khác nhau giữa interface và abstract class
Điểm chung đều thể hiện tính trừu tượng.

|  | Interface | Abstract class |
|---|---|---|
| Khai báo | Interface phải dùng từ khóa impliment | Abstract class phải dùng từ khóa extend |
| Số lượng kế thừa | Interface được nhiều | Abstract classextend được 1  |
| Access modifile | Mặc định access modifile của Interface là public | Abstract class có thể lựa chọn public, private, default, protect  |
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
- @Component: chú thích trên class
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

- Là một mẫu thiết kế phần mềm mà các đối tượng phụ thuộc sẽ được inject vào một lớp nào đó
- Mục đích tạo ra nhằm giảm phụ thuộc giữa các Class với nhau 
**VD: **

## Mối quan hệ giữa Dependency in version, Inversion of Control và Dependency injection (mối liên hệ giữa ba câu 8,9,10)

**VD: 
