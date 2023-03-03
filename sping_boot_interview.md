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
| Mô tả dễ hiểu | Là 1 modun nằm trong Spring framework | Là 1 modun nằm trong Spring framework và là 1 thằng trong Spring boot |
| Mô tả trực quan | Spring Boot là một framework giúp cho việc phát triển ứng dụng Spring trở nên đơn giản và nhanh chóng hơn bằng cách cung cấp sẵn các cấu hình mặc định và tích hợp các công nghệ phổ biến như Spring MVC, Spring Data, Spring Security,... trong một package duy nhất. Spring Boot cung cấp các cấu hình mặc định và tích hợp các công nghệ phổ biến | Spring MVC là một phần trong Spring Framework, cung cấp các class và annotation để xây dựng ứng dụng web theo kiến trúc MVC (Model-View-Controller). Các class và annotation của Spring MVC giúp cho việc xử lý request và trả về response trở nên đơn giản và dễ dàng hơn. Ngoài ra, Spring MVC còn cung cấp các tính năng như validation, exception handling, data binding,... giúp cho việc phát triển ứng dụng web trở nên thuận tiện hơn. |

***Các annotation như @Controller, @RestController, @RequestMapping, @GetMapping, @PostMapping,... chính là các annotation của Spring MVC***

***Tóm lại: Spring Boot cung cấp các cấu hình mặc định và tích hợp các công nghệ phổ biến, trong khi Spring MVC cung cấp các class và annotation để xây dựng ứng dụng web theo kiến trúc MVC***

Hiện nay có 2 cách xây dựng mô hình MVC: 
 - Kiểu xây dụng thuần túy (cấu hình bằng tay, cần cái gì làm cái gì sẽ add cái đó. **VD: để cấu hình được server thì cần cài concat còn Spring boot đã có sẵn rồi**)
 - Dùng Spring boot để build (tự động cấu hình sẵn, cụ thể là tự động tạo dựa theo Spring MVC giống như laravel và php)
 
# 4. Khái niệm tight-coupling (liên kết ràng buộc) và cách loosely couple
 - tight-coupling hay "liên kết ràng buộc" là một khái niệm trong Java ám chỉ việc mối quan hệ giữa các Class quá chặt chẽ. Khi yêu cầu thay đổi logic hay một class bị lỗi sẽ dẫn tới ảnh hưởng tới toàn bộ các Class khác.

 - loosely-coupled là cách ám chỉ việc làm giảm bớt sự phụ thuộc giữa các Class với nhau.

# 5. DI (Dendency Injection) là gì?
- Là 1 kỹ thuật lập trình giúp cho các class không bị phụ thuộc vào nhau(giảm việc sử dụng new). Nó cho phép các class phụ thuộc vào các interface hoặc abstract class thay vì phụ thuộc vào các class cụ thể, từ đó làm tăng tính linh hoạt và khả năng tái sử dụng của mã.
- Ví dụ cách sử dụng Constructor Injection:
  ```sh
  public class MyService {
    private MyDependency myDependency;

    public MyService(MyDependency myDependency) {
        this.myDependency = myDependency;
    }

    public void doSomething() {
        myDependency.doSomethingElse();
    }
   }

   public interface MyDependency {
       void doSomethingElse();
   }

   public class MyDependencyImpl implements MyDependency {
       public void doSomethingElse() {
           System.out.println("Doing something else.");
       }
   }
  ```
  Ở đây, lớp MyService có một thuộc tính MyDependency và một constructor được sử dụng để thiết lập MyDependency. Lớp MyDependency có một phương thức doSomethingElse() để thực hiện một hành động
  Để sử dụng MyService, chúng ta có thể làm như sau
  ```sh
  MyDependency myDependency = new MyDependencyImpl();
  MyService myService = new MyService(myDependency);
  myService.doSomething();
  ```
  Khi đó, kết quả sẽ là in ra dòng chữ "Doing something else.". Trong trường hợp này, MyDependency được truyền vào qua constructor của MyService thay vì thông qua một phương thức setter
  
- Ví dụ cách sử dụng Setter Injection: 
  ```sh
  public class UserService {
    private UserRepository userRepository;

    public void setUserRepository(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public List<User> getAllUsers() {
        return userRepository.getAllUsers();
    }

    // Other methods
  }
  ```
  Trong ví dụ này, ta sử dụng Setter Injection để truyền đối tượng UserRepository vào UserService. Ta tạo một setter method để thiết lập đối tượng UserRepository cho UserService. Ta có thể sử dụng method này để thiết lập đối tượng UserRepository từ bên ngoài UserService. Như vậy, ta cũng đã giảm sự phụ thuộc của UserService vào UserRepository.
  Để sử dụng UserService, ta có thể sử dụng code sau:
  ```sh
  UserRepository userRepository = new UserRepositoryImpl();
  UserService userService = new UserService();
  userService.setUserRepository(userRepository);
  List<User> users = userService.getAllUsers();
  ```
  
 - Ví dụ cách sử dụng Interface Injection: 
  
  Giả sử chúng ta có interface MessageService và hai implementation của nó là EmailService và SMSService. Chúng ta sử dụng interface injection để thực hiện gửi tin nhắn trong NotificationService.
  ```sh
  public interface MessageService {
    void sendMessage(String message);
  }

  public class EmailService implements MessageService {
      public void sendMessage(String message) {
          System.out.println("Sending email: " + message);
      }
  }

  public class SMSService implements MessageService {
      public void sendMessage(String message) {
          System.out.println("Sending SMS: " + message);
      }
  }

  public class NotificationService {
      private MessageService messageService;

      public NotificationService(MessageService messageService) {
          this.messageService = messageService;
      }

      public void sendNotification(String message) {
          messageService.sendMessage(message);
      }
  }
  ```
  Chúng ta có thể sử dụng NotificationService như sau:
  ```sh
  public static void main(String[] args) {
    MessageService emailService = new EmailService();
    NotificationService notificationService = new NotificationService(emailService);
    notificationService.sendNotification("Hello from email!");

    MessageService smsService = new SMSService();
    notificationService = new NotificationService(smsService);
    notificationService.sendNotification("Hello from SMS!");
  }
  ```
  Ở đây, chúng ta không trực tiếp khởi tạo các implementation của MessageService trong NotificationService, mà chúng ta khởi tạo các implementation đó ngoài và truyền chúng vào NotificationService thông qua constructor. Điều này giúp chúng ta giảm sự phụ thuộc của NotificationService vào các implementation cụ thể của MessageService.
  
# 6. IoC (Inversion of Control) là gì?
- Inversion of Control có thể hiểu là một nguyên lý thiết kế trong công nghệ phần mềm dựa trên kỹ thuật lập trình DI (Dendency Injection).  Các kiến trúc phần mềm được được áp dụng thiết kế này sẽ được **đảo ngược quyền điều khiển so với kiểu lập trình hướng thủ tục**. Mục đích là để tránh việc khởi tạo new.
- Thay vì class A phải phụ thuộc chờ class B khởi tạo
  ```sh
  public class A {
      private B b;
      
      public A (B b) {
          this.b = b;
      }
      
      public void doSomething(){
         return b.hello();
      }
  }
  
  public class B {
      private B b;
      
      public void hello(){
         return "hello";
      }
  }
  ```
- Thay thì ta chỉ cần ném vào IOC container để quản lý. Sau khi chạy chương trình, tất cả khai báo Bean đều được khởi tạo 1 lần duy nhất. Khi class A gọi đến B, thì @Autowire sẽ chạy vào trong IOC container để tìm thằng bean nào tên là B. Như vậy class A sẽ không phải lo việc chờ khởi tạo B.
```sh
  public class A {
      @Autowire
      private B b;
      
      public void doSomething(){
         return b.hello();
      }
  }
  
  @Component
  public class B {
      private B b;
      
      public void hello(){
         return "hello";
      }
  }
  ```

- Ví dụ: Ta đăng ký đối tượng UserService với Spring Container
  ```sh
  @Configuration
  public class AppConfig {

      @Bean
      public UserService userService() {
          return new UserServiceImpl();
      }
  }
  ```
  Tiếp theo, sử dụng UserService trong một đối tượng khác
  ```sh
  @Service
  public class UserController {

      private UserService userService;

      @Autowired
      public UserController(UserService userService) {
          this.userService = userService;
      }
  }
  ```
  Ở đây, đối tượng UserController sử dụng UserService để thực hiện một số tác vụ. Spring tự động đưa UserService đến constructor của UserController khi tạo đối tượng, thay vì UserController phải tạo ra đối tượng UserService bằng tay. Việc này giúp giảm thiểu sự phụ thuộc giữa các đối tượng trong ứng dụng
  
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
| Mô tả | Là 1 kỹ thuật lập trình dùng để tách logic chương trình thành các phần riêng biệt, VD: mình muốn xử lý riêng modul exception AplicationException trả về báo lỗi theo ý mình. AOP sẽ làm nhiệm vụ sẽ xem AplicationException trong chương trình mà không có try cacth | Là phương pháp lập trình dựa trên khái niệm về lớp và đối tượng |

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
- Java Persistence API là 1 quy chuẩn chung để làm việc với tất cả database qua việc sử dụng các đối tượng thay vì phải truy vấn SQL trực tiếp.
(Đặc điểm nhận biết )

# 21. Spring JPA là gì?
- Được xây dựng dựa trên JPA. Là một phần trong hệ sinh thái Spring Data, nó tạo ra một layer ở giữa tầng service và database, giúp chúng ta thao tác với database một cách dễ dàng hơn, tự động config và giảm thiểu code thừa thãi.

# 22. ORM là gì?
- ORM(Object Relational Mapping: Ánh xạ quan hệ đối tượng)
- Object-Relational-Mapping là 1 framework cho phép chuyển đổi từ các object trong lập trình OOP sang database quan hệ và ngược lại.
- Là 1 kỹ thuật lập trình giúp ánh xạ cơ sở dữ liệu sang dạng đối tượng class

# 21. Hibernate là gì?
- Là 1 framework của ORM cho phép map các objects trong class để truy vấn tạo bảng. Được xây dựng dựa trên JPA, và có chức năng tương tự như JPA nhưng Hibernate cung cấp các tính năng mở rộng hơn so với JPA.
- VD Sử dụng hibernate để thực hiện cache data và tối ưu hoá hiệu suất truy vấn cơ sở dữ liệu để cấu hình tùy chọn mở rộng: 
  - Sử dụng hibernate để thực hiện các truy vấn đặc biệt như truy vấn theo nhiều điều kiện khác nhau
  ```sh
  public interface UserRepository extends JpaRepository<User, Long> {

    @Query("SELECT u FROM User u WHERE u.name = :name AND u.age = :age")
    List<User> findByNameAndAge(@Param("name") String name, @Param("age") int age);
  }
  ```
  
  - Sử dụng hibernate để thực hiện cache data và tối ưu hoá hiệu suất truy vấn cơ sở dữ liệu
  ```sh
  @Cache(usage = CacheConcurrencyStrategy.READ_ONLY)
  @Entity
  public class User {
      @Id
      private Long id;
      private String name;
  }
  ```

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

# 23. Fecth LAZY và EAGER là gì?
>>![](https://stackjava.com/wp-content/uploads/2017/11/hibernate-1-1.png)
- LAZY: Không lấy dữ liệu từ các bảng liên quan. Ví dụ nếu lấy dữ liệu bảng Company thì sẽ không lấy thêm dữ liệu gì khác
- EAGER: Lấy dữ liệu từ các bảng liên quan. Ví dụ nếu lấy dữ liệu bảng Company thì sẽ lấy dữ liệu bảng liên quan là Employee

# 24. Nguyên lý solid?
Là một tập hợp các nguyên tắc thiết kế phần mềm, mục đích là để giúp dễ bảo trì và tái sử dụng hơn gồm:
- Single Responsibility Principle (SRP): Một class nên chỉ có một trách nhiệm duy nhất.
- Open-Closed Principle (OCP): Các class, module và phần mềm nên được thiết kế để có thể mở rộng, nhưng không làm ảnh hưởng chức năng hiện tại.
- Liskov Substitution Principle (LSP): Các object của một subclass nên có thể thay thế được object của superclass mà không làm thay đổi tính đúng đắn của chương trình.
- Interface Segregation Principle (ISP): Các interface lớn tách thành các interface nhỏ hơn, nhằm giảm sự phụ thuộc và tăng tính linh hoạt của hệ thống.
- Dependency Inversion Principle (DIP): Các class không phụ thuộc lẫn nhau. Nguyên tắc này khuyến khích việc sử dụng dependency injection để tách các phụ thuộc và giảm sự phụ thuộc của các class

# 25. Các annotation chính trong Spring MVC bao gồm:

@Controller: được sử dụng để đánh dấu một class là một controller trong Spring MVC.

@RequestMapping: được sử dụng để ánh xạ một URL đến một phương thức xử lý trong controller.

@PathVariable: được sử dụng để trích xuất giá trị từ URL và gán vào một tham số của phương thức xử lý.

@RequestParam: được sử dụng để trích xuất giá trị từ các tham số của request và gán vào một tham số của phương thức xử lý.

@ResponseBody: được sử dụng để đánh dấu một phương thức trả về dữ liệu là response body chứ không phải view.

@ModelAttribute: được sử dụng để đưa các đối tượng vào model và chuyển đến view.

@SessionAttribute: được sử dụng để lưu trữ một đối tượng trong session.

@InitBinder: được sử dụng để cấu hình một đối tượng Binder cho phép thực hiện data binding.


# 26. Code VD về sự khác nhau giữa Hibernate và JPA:
- sử dụng JPA: 
```sh
@Entity
@Table(name = "employees")
public class Employee {
    
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;
    
    private String name;
    
    // getters and setters

}
```
```sh
@Repository
public class EmployeeRepository {

    @PersistenceContext
    private EntityManager entityManager;
    
    public Employee findById(Long id) {
        return entityManager.find(Employee.class, id);
    }
    
    public void save(Employee employee) {
        entityManager.persist(employee);
    }
    
    public void delete(Employee employee) {
        entityManager.remove(employee);
    }
    
    // other methods
    
}
```

- sử dụng Hibernate:
```sh
@Entity
@Table(name = "employees")
public class Employee {
    
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;
    
    private String name;
    
    // getters and setters

}
```
```sh
@Repository
public class EmployeeRepository {

    @Autowired
    private SessionFactory sessionFactory;
    
    public Employee findById(Long id) {
        Session session = sessionFactory.getCurrentSession();
        return session.get(Employee.class, id);
    }
    
    public void save(Employee employee) {
        Session session = sessionFactory.getCurrentSession();
        session.save(employee);
    }
    
    public void delete(Employee employee) {
        Session session = sessionFactory.getCurrentSession();
        session.delete(employee);
    }
    
    // other methods
    
}
```
trong JPA sử dụng EntityManager để truy vấn còn Hibernate dùng SessionFactory. Hibernate là một implementation của JPA, vì vậy nó có thể được sử dụng như một thay thế cho JPA. Tuy nhiên, khi sử dụng Hibernate, ta sẽ phải sử dụng những đối tượng được cung cấp bởi Hibernate như SessionFactory và Session thay vì EntityManager.

***nếu ta sử dụng các annotation và API được định nghĩa trong gói javax.persistence, thì bạn đang sử dụng JPA. Nếu bạn sử dụng các annotation và API được định nghĩa trong gói org.hibernate, thì bạn đang sử dụng Hibernate.***
