## 1. Khác nhau giữa interface và abstract class
Điểm chung đều thể hiện tính trừu tượng.

|  | Interface | Abstract class |
|---|---|---|
| Khai báo | Interface phải dùng từ khóa impliment | Abstract class phải dùng từ khóa extend |
| Số lượng kế thừa | Interface được nhiều | Abstract classextend được 1  |
| Access modifile | Mặc định access modifile của Interface là public | Abstract class có thể lựa chọn public, private, default, protect  |
| Chứa bên trong | Interface chỉ chứa hàm | Abstract có chứa thuộc tính, function implementation **(function abtract)** , function chi tiết  |
| Thường sử dụng | Interface thể hiện 100% tính trừu tượng nên hay dùng làm bản phác thảo giúp cho các tính năng ko bị thiếu | Abstract class thường dùng khi muốn các class con kế thừa đến có thể sử dụng chung hàm, ngoài ra cho phép chứa các thuộc tính giới hạn truy cập access modifile |

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
