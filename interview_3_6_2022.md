### 1.Tại sao java là nn độc lập nền tảng

- Vì *__trình biên dịch Java là jvm(java virtural machine)__* giúp cho chương trình java chạy tốt 
- các nền tảng khác nhau (cụ thể là hệ điều hành như window, mac,linux,...)

### 2.Tại sao lại dùng bản jdk 8 

- Là vì tính ổn định cần khi phát triển sản phẩm

### 3.Tính năng của jdk 8

- Lamda, tream, colection api, for each, colcurency

### 4.Đa hình: cùng 1 phương thức được thể hiện theo nhiều cách khác nahu
#### 4.1 Overloading, Đa hình tĩnh: (compile time polymorphism)

- Tại thời điểm gọi đến hàm,  ta biết phải truyền tham số gì. Cùng kết quả trả về nhưng tham số truyền vào khác nhau về kiểu dữ liệu, số lượng, vị trí.

#### 4.2 Overiding, Đa hình động: (run time type polymorphism)

- Tại thời điểm chạy chương trình, thể hiện theo nhiều cách khác nhau. 1 hàm Cùng tham số truyền vào, cùng 1 kết quả trả về nhưng được thể hiện nhiều cách khác nhau. 
*Thể hiện ở chỗ khi 1 phương thức được viết lại theo nhiều cách khác nhau ở trên lớp con là nhưng lớp được impliment hoặc extend từ lớp cha, 
cùng 1 phương thức đó nhưng được thể hiện nhiều cách khác* 

### 5.Heap, stack trong java

- heap(lỗi: out of memory: tràn bộ nhớ, xảy ra khi tạo new đối tượng không đủ): chứa các kiểu dữ liệu **object**  
- stack(stack overflow): nhỏ hơn heap, thường lưu kiểu dữ liệu nguyên thủy

### 6.Luồng

- Khi cần chương trình chạy nhanh hơn

### 7.@transactional

- Khi 2 thằng gọi đến nhau thì nó sẽ chỉ là 1(defaul là v). Nếu muốn tách ra thì sẽ có funcion để tách
Khi tương tác vs db nếu lỗi giữa chùng thì sẽ rollback lại

**VD: Khi insert 100 nhưng nếu đến 5 lỗi thì sẽ quay lại từ đầu(hoặc vào all hoặc ko vào). Tức là 1 là 100 thằng vào cùng 1 lúc còn 2 không có thằng nào vào vì lỗi**

### 8.Sự khác nhau giữa == và equal

- equal: so sánh nội dung
- ==: so sánh địa chỉ **(lưu ý phải là object, ko bị gặp lỗi null queter exeption)**

### 9.Lợi ích dùng Interface

- Tính bao quát
- Dễ bảo trì

### 10.Tham chiếu và tham trị trong Java

- Tham chiếu (pass by reference): truyền theo tham chiếu **(gọi đến địa chỉ của đối tượng, cụ thể ở đây là Reference Types (những biến có kiểu dữ liệu class, cứ new là sẽ tạo ra 1 vùng nhớ bên heap)**
- Tham trị (pass by value): truyền theo giá trị **(xảy ra khi gọi đến 1 hàm và truyền giá trị cho hàm đó)**

### 11.Kiểu dữ liệu Enum

- Giới hạn giá trị sử dụng, tránh những giá trị không mong muốn VD status

### 12.Reflection trong java

- Giúp xem tất cả thông tin trong class. Vấn đề nằm ở chỗ ta có thể nhìn sâu vào trong class mà ko cần biết class đó có gì
**VD: khi ta viết 1 class mà dành cho tất cả các thể loại class khác nhau**
**VD điển hình là @Autowire**
- (Ko còn vì dùng framework)(autowired)(nguy hiểm, gây những lỗi ko xác định)
Vd: khi extend JpaRepos có thể truyền vào dù là cus, std
- Là một cách nhìn lại tất cả tt trong class
- Nhìn sâu vào class mà ko cần bt là class j

### 13.Generate type

- Là tham số hóa kiểu dữ liệu
**VD: array list**

### 14.Spring profile
- Được sử dụng để test

### 15.fail-fast và fail-safe

- Là quá trình lỗi xảy ra khi mà ta làm việc với tập hợp các phần tử mà ta sửa hoặc xóa các phần tử bên trong

### 16.Builer design pattern

- Thay vì khởi tạo nhiều constructor **(VD: Student(int id, string name) hay Student(int id) )** với các tham số truyền vào, thì ta chỉ cần làm trên 1 dòng lệnh với **Builder**
- Khi ta dùng **Builer** thì ta có thể sử dụng tạo ra obj đơn giản Thay vì làm việc trên nhiều dòng lệnh
thì sẽ làm trên 1 dòng
**VD: (.name.rollNumber.email.build()) => 1 Obj** 

### 17.Singertern pattern

- Đảm bảo đối tượng đó được tạo 1 lần duy nhất
- Là những thằng như getConnection(), getInstant() luôn luôn là 1 hàm static để đảm bảo đối tượng đó được tạo 1 lần duy nhất
**vd: if connection == null || connection.isClose() thì sẽ tạo mới, còn else thì trả về luôn connection**

### 18.List và mảng

- List có thể mở rộng phần tử
- mảng cố định các phần tử

### 19.Hashset

- Hashset không thể phân biệt được các đối tượng.
- Vấn đề với Hashset xảy ra khi ta **Add hay Put vào 1 số nguyên thì Add 2 số 5 thì sẽ thành 1 số 5 hay Add 2 Hùng thì sẽ trở thành 1 Hùng.**
*Nhưng nếu ta add 2 đối tượng student có cùng mã id giống nhau thì nó sẽ tạo ra 2 đối tượng khác nhau 
- Để giải quyết vấn đề phân biệt đối tượng khác nhau thì ta phải ghi đè lại 2 thằng là compareTo() và hashCode() 
**VD: trong compareTo() chỉ cần 1 thằng rollNumber nó trùng nhau trong Student thì nó là 1 Student**

### 20.Dấu ... trong function

- Cho phép truyền bất cứ tham số nào vào. Tạo sự dynamic
