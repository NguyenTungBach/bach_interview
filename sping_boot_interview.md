# 1. Spring là gì?
 - ### Cách hiểu chung trên mạng
Spring là một **framework** mã nguồn mở được phát triển dựa trên nền tảng là Java, giúp đơn giản hóa việc xây dựng và phát triển các ứng dụng java doanh nghiệp
 - ### Cách hiểu chung của mình
Thông qua cách hiểu Framework **(thư viện)** thì ta có thể hiểu Spring Framework giúp lập trình viên Java phát triển web 1 cách dễ dàng, nhanh chóng và đơn giản hóa.
>>![](https://images.viblo.asia/94b1b009-62b1-49e8-ae95-fccc0db1f9d3.png)

# 2. Spring boot là gì?
Spring Boot là một module nằm trong Spring Framework được sử dụng rộng rãi để phát triển các REST APIs. Spring Boot giúp:
- Đơn giản hóa bước cấu hình (thay vì XML thì dựa trên annotation)
- Dễ dàng triển khai trên Server vì được nhúng sẵn trong ứng dụng
- Cung cấp tập hợp starter dependencies giúp dev dễ dàng hơn trong việc phát triển ứng dụng

Các thành phần trong Spring Boot:
- Spring Web Service (đặc điểm nhận dạng @RestController): 
- Spring Sercurity (đặc điểm nhận dạng @EnableWebSecurity): cung cấp đăng nhập và phân quyền
- Spring Data (đặc điểm nhận dạng Spring Data JPA): truy vấn, thêm, sửa, xóa dữ liệu

# 3. Phân biệt Spring boot và Spring MVC
- Cùng nằm trong Spring Framework

|  | Spring boot | Spring MVC |
|---|---|---|
| Mô tả dễ hiểu | Là công nghệ | Mô hình (degin parten) |
| Mô tả trực quan | Là công nghệ và công nghệ này có thể dùng để xây dựng dựa theo mô hình String MVC hoặc có thể dùng để viết API | Degin parten này có rất nhiều công nghệ được sử dụng trong đó có Spring Framework, thì Spring Framework dùng thằng MVC này để tạo ra Spring MVC để nó xây dựng Web site |

Hiện nay có 2 cách xây dựng mô hình MVC: 
 - Kiểu xây dụng thuần túy (cấu hình bằng tay, cần cái gì làm cái gì sẽ add cái đó. **VD: để cấu hình được server thì cần cài concat còn Spring boot đã có sẵn rồi**)
 - Dùng Spring boot để build (tự động cấu hình sẵn, cụ thể là tự động tạo dựa theo Spring MVC giống như laravel và php)
 
# 4. Khái niệm tight-coupling (liên kết ràng buộc) và cách loosely couple
 - tight-coupling hay "liên kết ràng buộc" là một khái niệm trong Java ám chỉ việc mối quan hệ giữa các Class quá chặt chẽ. Khi yêu cầu thay đổi logic hay một class bị lỗi sẽ dẫn tới ảnh hưởng tới toàn bộ các Class khác.

 - loosely-coupled là cách ám chỉ việc làm giảm bớt sự phụ thuộc giữa các Class với nhau.

# 5. DI (Dendency Injection) là gì?
- Là 1 kỹ thuật lập trình giúp cho các class không bị phụ thuộc vào nhau

# 6. IoC (Inversion of Control) là gì?
- Inversion of Control có thể hiểu là một nguyên lý thiết kế trong công nghệ phần mềm. Các kiến trúc phần mềm được được áp dụng thiết kế này sẽ được **đảo ngược quyền điều khiển so với kiểu lập trình hướng thủ tục**

- Để có thể hiểu rõ hơn về IoC, ta có thể lấy một ví dụ như sau: Giả sử có 1 class mẹ là A và hai class con là B và C ( lúc này B và C sẽ được gọi là các dependencies)
Với mô hình không sử dụng IoC thì Class A cần phải khởi tạo và điều khiển hai class B và C, bất kỳ thay đổi nào ở Class A đều dẫn đến thay đổi ở Class B và C. Một thay đổi sẽ kéo theo hàng loạt những thay đổi khác từ đó làm giảm khả năng bảo trì của code. Trong khi đó, nếu trong mô hình sử dụng IoC, các class B và C sẽ được đưa đến độc lập so với class A thông qua một bên thứ ba, từ đó các class không phụ thuộc lẫn nhau mà chỉ phụ thuộc vào interface. Điều này cũng đồng nghĩa rằng sự thay đổi ở class cấp cao sẽ không ảnh hưởng tới các class cấp thấp hơn
![N|Solid](https://xuanthulab.net/photo/ioc-4477.png)

# 7. Application Context là gì?
- Là khái niệm Spring Boot dùng để chỉ Spring IoC container, tương tự như bean là đại diện cho các dependency.
- Khi ứng dụng Spring chạy, Spring IoC container sẽ quét toàn bộ packages, tìm ra các bean và đưa vào ApplicationContext.

# 8. Bean là gì?
- Bean là những class mà mình sử dụng trong project. Khi khai báo Bean sẽ được IOC trong spring quản lý các Bean đó.

# 9. Spring container (IoC Container) là gì?
- Quản lý vòng chạy của Bean: khởi tạo, cấu hình và tương tác giữa các Bean

# 10. Bean Factory và ApplicationContext interface
BeanFactory và ApplicationContext interface là 2 interface đại diện và để khởi tạo cho cho Spring IoC container

|  | Bean Factory | ApplicationContext Interface |
|---|---|---|
| Mô tả | Là root interface dùng để thao tác với Spring container, nó cung cấp những tính năng cơ bản để quản lý bean trong ứng dụng | là một sub-interface của BeanFactory, vì vậy nó cung cấp tất cả các tính năng trong BeanFactory |

# 10. Các cách khởi tạo bean
Các cách tạo bean
 - @Bean: chú thích trên hàm
 - @Component: chú thích trên class
 - @Repository: chú thích cho class giúp truy vấn dữ liệu database
 - @Service: chú thích cho class xử lý logic
 - @Controller: chú thích class làm việc với Request

# 11. Lập trình hướng khía cạnh AOP và lập trình hướng đối tượng OOP

|  | AOP (Aspect Oriented Programming) | OOP (Object Oriented Programming) |
|---|---|---|
| Mô tả | Kiểu lập trình cho phép tách các module (chia nhỏ và dùng lại) | Là phương pháp lập trình dựa trên khái niệm về lớp và đối tượng |

# 12. @Autowired
- Đánh dấu cho Spring biết rằng sẽ tự động inject bean tương ứng vào vị trí được đánh dấu.
>>Trong thực tế, sẽ có trường hợp chúng ta sử dụng @Autowired khi Spring Boot có chứa 2 Bean cùng loại trong Context. Lúc này thì Spring sẽ bối rối và không biết sử dụng Bean nào để inject vào đối tượng. Có 2 cách để giải quyết vấn đề này: @Primary và Qualifier

 # 13. @Primary
 - Là annotation đánh dấu trên một Bean, giúp nó luôn được ưu tiên lựa chọn trong trường hợp có nhiều Bean cùng loại trong Context
 
 # 14. @Qualifier
 - Xác định tên của một Bean mà bạn muốn chỉ định inject
 
 # 15. @RestController
 - Khác với @Controller là sẽ trả về một template. @RestController trả về dữ liệu dưới dạng JSON.
 
 # 16. CORS trong Spring Boot?
 - CORS là viết tắt của Cross-Origin Resource Sharing là một cơ chế được thực hiện bởi các trình duyệt và giúp người dùng cho phép các yêu cầu giữa các miền

# 17. CSRF là gì?
- là kỹ thuật tấn công bằng cách sử dụng quyền chứng thực của người dùng đối với một website.
- Hiểu đơn giản, đây là kỹ thuật tấn công dựa vào mượn quyền trái phép

# 18. @Data là gì?
- Gồm sẽ biên dịch @Getter, @Setter, @RequiredArgsConstructor, @ToString và @EqualsAndHashCode
Vấn đề hàm toString: nó sẽ gọi đến những thuộc tính không mong muốn ví dụ như thuộc tính của mình là
class khác. Nếu chẳng may mà class được gọi đó lại có gọi đến thuộc tính của class mà mình đang
gọi => sẽ dẫn đến vòng lặp vô tận

# 19. Java JDBC
- Là một Java API được sử dụng để kết nối và thực hiện truy vấn với cơ sở dữ liệu. Nhưng cần ghi rõ Select * From Where ... **(Hồi kỳ 2 đã học)**
- Là một thư viện xây dựng từ Java Core giúp kết nối cơ sở dữ liệu

# 20. JPA là gì?
- Java Persistence API là 1 quy chuẩn chung để làm việc với tất cả database 
(Đặc điểm nhận biết )

# 21. Spring JPA là gì?
- Được xây dựng dựa trên JPA. Là một phần trong hệ sinh thái Spring Data, nó tạo ra một layer ở giữa tầng service và database, giúp chúng ta thao tác với database một cách dễ dàng hơn, tự động config và giảm thiểu code thừa thãi.

# 22. ORM là gì?
- Object-Relational-Mapping là 1 framework cho phép chuyển đổi từ các object trong lập trình OOP sang database quan hệ và ngược lại.

# 21. Hibernate là gì?
- Là 1 framework của ORM cho phép map các objects trong class để tạo bảng

# 22. Các scope trong spring?
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


