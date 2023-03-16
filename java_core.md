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

**VD Ngày mai tôi muốn dùng trên thằng này ngày kia tôi muốn dùng thằng khác. Thì tôi phải dùng
interface để khai báo. Vì lúc cần mình có thể dễ dàng thay đổi**


### 10.Tham chiếu và tham trị trong Java

- Tham chiếu (pass by reference): truyền theo tham chiếu **(gọi đến địa chỉ của đối tượng, cụ thể ở đây là Reference Types (những biến có kiểu dữ liệu class, cứ new là sẽ tạo ra 1 vùng nhớ bên heap)**
- Tham trị (pass by value): truyền theo giá trị **(xảy ra khi gọi đến 1 hàm và truyền giá trị cho hàm đó)**

### 11.Kiểu dữ liệu Enum

- Giới hạn giá trị sử dụng, tránh những giá trị không mong muốn VD status

### 12.Reflection trong java

- Giúp xem tất cả thông tin trong class. Vấn đề nằm ở chỗ ta có thể nhìn sâu vào trong class mà ko cần biết class đó có gì
- Hỗ trợ cho ta có thể viết một đoạn code mà có thể dùng lại được cho các class khác nhau
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

### 21.JWT là gì

- Dùng để tạo ra token thông qua thuật toán mã hóa
- Cấu trúc gồm 3 phần: header, payload, signature
- *Header*: chứa kiểu dữ liệu và thuật toán sử dụng để mã hóa JWT 
  - VD: {
    "typ": "JWT",
    "alg": "HS256"
    } 
- *Payload*: chứa các thông tin mình muốn đặt trong chuỗi token như username, password,...
- *Signature*: chữ ký mã hóa. Phần chử ký này sẽ được tạo ra bằng cách mã hóa phần **header** , **payload** kèm theo một chuỗi **secret (khóa bí mật)**

### 22.Sự khác nhau giữa equal và hashcode
- equal được sử dụng để so sánh hai đối tượng với nhau
- hashcode  trả về một giá trị băm số nguyên (integer) được tính toán dựa trên các thuộc tính của đối tượng. Mục đích là để tính toán giá trị cho các cấu trúc dữ liệu như HashMap hoặc HashSet
  - Ví dụ khi thêm một cặp key value trong HashMap. Nó sẽ tính toán giá trị của cặp key value bằng hashCode. Khi truy vấn một key, HashMap sẽ băm dựa trên hashcode và tìm đến giá trị trùng với hashcode đó
  - Trường hợp hai key khác nhau giá trị hashcode bị trùng:
  ```sh
  class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public int hashCode() {
        return age % 10; // giá trị băm được tính dựa trên tuổi của người
    }

    @Override
    public boolean equals(Object obj) {
        if (obj == this) {
            return true;
        }
        if (!(obj instanceof Person)) {
            return false;
        }
        Person other = (Person) obj;
        return this.age == other.age && this.name.equals(other.name);
    }
    }

    Map<Person, String> map = new HashMap<>();
    map.put(new Person("John", 25), "John's value");
    map.put(new Person("Mary", 35), "Mary's value");
    map.put(new Person("Dave", 15), "Dave's value");
    map.put(new Person("Jane", 25), "Jane's value");

  ```
    Ở ví dụ trên, ta định nghĩa một lớp Person có hai thuộc tính name và age. Phương thức hashCode() được định nghĩa dựa trên thuộc tính age của người, trả về giá trị băm là age % 10. Phương thức equals() được định nghĩa để so sánh hai đối tượng Person dựa trên cả name và age. 
    
    Sau khi thêm các đối tượng Person vào HashMap, ta có bảng băm như sau:
    
    ```sh
    Index 0:
    - Person{name='Dave', age=15} -> "Dave's value"
    Index 5:
    - Person{name='John', age=25} -> "John's value"
    - Person{name='Jane', age=25} -> "Jane's value"
    Index 8:
    - Person{name='Mary', age=35} -> "Mary's value"

    ```
    Như vậy, ta có hai đối tượng Person có cùng giá trị băm là 5, đó là John và Jane. Chúng được lưu trữ trong cùng một vị trí và được đánh dấu bằng dấu mũi tên trong bảng băm. Khi truy vấn giá trị của John, HashMap sẽ duyệt qua danh sách liên kết tại vị trí này và trả về giá trị của John. Tương tự, khi truy vấn giá trị của Jane, HashMap cũng sẽ tìm kiếm
    
### 23. Các thành phần chính trong OOP:
- Kế thừa: Lớp con kế thừa thuộc tính và các hàm của lớp cha
- Đóng gói: che giấu dữ liệu của một lớp
- Đa hình: Một phương thức nhưng được thể hiện theo nhiều cách khác nhau
- Trừu tượng: Là bước phác thảo đảm bảo các tính năng không bị thiếu

### 24. Equals và Contain:
- Equals so sánh giá trị của đối tượng
- Contain kiểm tra chuỗi đó có chứa một chuỗi con hay không

### 25. Vì sao String là một kiểu dữ liệu đối tượng nhưng so sánh equals vẫn là true còn nếu là đối tượng class thông thường sẽ thành false?
- Mặc định khi so sánh đối tượng trong equals sẽ là so sánh địa chỉ bộ nhớ nên cần phải ghi đè
- Còn String bản thân nó đã có quy định với hàm equal nên sẽ so sanh theo giá trị

## 26. Khác nhau giữa String, String Builder và String Buffer
- String khi khởi tạo mới sẽ dùng bộ nhớ mới
- Builder và buffer khi khởi tạo không dùng bộ nhớ mới mà ghi đè vào bộ nhớ cũ
- String builder và String buffer có trong mutable object (thay đổi được giá trị) còn string thì ở trong immutable object(không thay đổi được giá trị)

- String builder là bất đồng bộ nên khi append có thể sẽ nối không đúng thứ tự. VD:
  ```sh
  StringBuilder sb = new StringBuilder();
  Thread thread1 = new Thread(() -> {
      sb.append("Hello");
  });

  Thread thread2 = new Thread(() -> {
      sb.append("World");
  });

  thread1.start();
  thread2.start();

  thread1.join();
  thread2.join();

  System.out.println(sb.toString());  
  ```
  Kết quả in ra có thể khác nhau mỗi lần chạy, ví dụ: "HelloWorld" hoặc "WorldHello". Để tránh vấn đề này, chúng ta có thể sử dụng các phương thức đồng bộ hóa trên StringBuilder để đảm bảo rằng các thao tác sẽ được thực hiện theo đúng thứ tự được mong đợi.

- String buffer là đồng bộ (thread safe) nên khi append chạy đa luồng  sẽ theo trình thứ tự. VD:
  ```sh
  StringBuffer sb = new StringBuffer();

  Thread thread1 = new Thread(() -> {
      sb.append("Hello");
  });

  Thread thread2 = new Thread(() -> {
      sb.append("World");
  });

  thread1.start();
  thread2.start();

  thread1.join();
  thread2.join();

  System.out.println(sb.toString());  
  ```
  Kết quả in ra sẽ luôn là "HelloWorld" bất kể thứ tự mà các luồng được thực thi, vì StringBuffer đảm bảo rằng các thao tác trên chuỗi sẽ được thực hiện tuần tự một cách đồng bộ.

**Nên khi nối chuỗi sẽ dùng String Builder. Nhưng chi khi nào nối nhiều chuỗi**
