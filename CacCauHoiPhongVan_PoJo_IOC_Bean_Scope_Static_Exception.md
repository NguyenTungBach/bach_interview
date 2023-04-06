### 1. Pojo là gì?
- Là các lớp cơ bản của java. Chỉ có constructor với getter và setter

### 2. IOC và DI?
- IOC dựa trên nguyên tắc ***(nguyên tắc là yêu cầu)*** solid. Trong nguyên tắc có nguyên lý ***(lý thuyết)*** DIP.
- Nguyên lý DIP chỉ ra các class không giao tiếp với nhau thông qua lớp triển khai (lớp implement gì gì đó) mà thống qua lớp trừu tượng (các interface, abtract)
- Dựa trên nguyên lý đó IOC (Đảo ngược quyền điều khiển) tạo ra IOC Container để quản lý sự phụ thuộc.
- Còn DI và IOC về bản chất nó giống nhau là để giảm sự phụ thuộc. DI là một trong những triển khai của IOC

### 3. Đảo ngược quyền điều khiển ở đây là gì?
- Thay vì mình tạo ra các lớp (khởi tạo new) để quản lý và dùng thì mình sẽ thông qua một thằng đảm nhận thay việc đó.

### 4. Bean là gì?
- Là một đối tượng được quản lý bởi IOC Container

### 5. Vòng chạy Bean là gì?
- B1: (Constructor) Khởi tạo
- B2: (Setter methods) inject các Bean
- B3: (Post Construct) Hành động chạy sau khi khởi tạo
- B4: (Pre Destroy) Trước khi hủy
- B5: (Destroy) Hủy Bean

### 6. Các cách khởi tạo bean?
- Anotation (thường dùng)
- XML
- JAVA BASE

### 7. Các cách khởi tạo bean bằng anotaion?
- @Bean: đặt trên hàm, kết quả của hàm này sẽ được IOC quản lý và trả về kết quả đó
- @Component: chú thích trên class, là một khuôn mẫu chung cho bất kỳ thành phần nào do Spring quản lý
- @Repository: chú thích cho class giúp truy vấn dữ liệu database
- @Service: chú thích cho class xử lý logic
- @Controller: chú thích class làm việc với Request

# 8. Các scope trong spring?
- Singleton: Các đối tượng trong bean chỉ được khởi tạo 1 lần duy nhất. Mặc định khi chạy bean là thằng này
```sh
VD:
@Scope("singleton")
public class Dress{
}
```

- Prototype: Các đối tượng trong bean được khởi tạo mỗi lần khi được gọi đến.
```sh
VD:
@Scope("prototype")
public class Dress{
}
```

- Request: giống với prototype scope, tuy nhiên nó dùng cho ứng dụng web, một thể hiện của bean sẽ được tạo cho mỗi HTTP request. Tức là mình truyền giá trị vào view nào thì view đó sẽ được truyền những giá trị đó

```sh
VD: request.setAttribute("username","Test")
```

- Session: Mỗi thể hiện của bean sẽ được tạo cho mỗi HTTP Session. Tức là các giá trị truyền vào view sẽ đc lưu vào session, nếu trong view đó ko có giá trị cần truyền thì nó sẽ kiểm tra xem trong session có ko

```sh
VD: 
HttpSession session = request.getSession();
session.setAttribute("username","Test")
```

- Application: Được sử dụng để tạo global sesion bean cho các ứng dụng Portlet. Tức là nếu mình tính toán trên view, mỗi lần refresh lại trang thì giá trị sẽ được thay đổi, đặc biệt thằng này có thể sử dụng trong bất cứ trang nào giông Session **(lưu ý là lấy giá trị, thực ra mình cũng có thể dùng tùy tình huống)**

```sh
VD: 
HttpSession application = request.getServletContext();
Integer hit = application.getAttribute("hitCounter")
if(hit == null || hit == 0){
 hit++;
}
application.setAttribute("hitCounter", hit)
```

# 8. Biến static (biến cục bộ)?
- Gọi được trực tiếp, không cần phải khởi tạo
- Cấp phát bộ nhớ chỉ xảy ra một lần nên tiết kiệm bộ nhớ

# 9. Hàm static ?
- Gọi được trực tiếp, không cần phải khởi tạo
- 1 phương thức static không gọi được this hay supper vì làm thế sẽ gọi đến instance của lớp
- 1 phương thức static không thể ghi đè vì nó là nó được gọi trực tiếp thông qua lớp chứ không phải qua đối tượng

# 10. static class (cho phép truy cập các thành viên dữ liệu tĩnh của lớp ngoài)
VD:
```sh
class TestOuter1 {
    static int data = 30;
 
    static class Inner {
        void msg() {
            System.out.println("data is " + data);
        }
    }
 
    public static void main(String args[]) {
        TestOuter1.Inner obj = new TestOuter1.Inner();
        obj.msg();
    }
}
```

# 11. Các loại exceptions:
- Checked exceptions: là những exception báo lỗi ngay trong khi code
- Unchecked exceptions: là những exception báo lỗi trong quá trình chạy
- Error: là một phần trong Unchecked exceptions, liên quan đến việc phần cứng không thể xử lý được
