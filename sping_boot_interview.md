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

Hiện nay có 2 kiểu xây dựng: 
 - Kiểu xây dụng thuần túy (cấu hình bằng tay, cần cái gì làm cái gì sẽ add cái đó )
 - Dùng Spring boot để build (tự động cấu hình sẵn, cụ thể là tự động tạo dựa theo Spring MVC giống như laravel và php)
 
# 4. Khái niệm tight-coupling (liên kết ràng buộc) và cách loosely couple
 - tight-coupling hay "liên kết ràng buộc" là một khái niệm trong Java ám chỉ việc mối quan hệ giữa các Class quá chặt chẽ. Khi yêu cầu thay đổi logic hay một class bị lỗi sẽ dẫn tới ảnh hưởng tới toàn bộ các Class khác.

 - loosely-coupled là cách ám chỉ việc làm giảm bớt sự phụ thuộc giữa các Class với nhau.

# 5. DI (Dendency Injection) là gì?
- Là 1 kỹ thuật lập trình giúp cho các class không bị phụ thuộc vào nhau

# 6. IoC (Inversion of Control) là gì?
- 

# 7. Application Context là gì?
- Là khái niệm Spring Boot dùng để chỉ Spring IoC container, tương tự như bean là đại diện cho các dependency.
- Khi ứng dụng Spring chạy, Spring IoC container sẽ quét toàn bộ packages, tìm ra các bean và đưa vào ApplicationContext.

# 8. Bean factory là gì?

# 9. Các cách khởi tạo bean
Các cách tạo bean
 - @Bean: chú thích trên hàm
 - @Component: chú thích trên class
 - @Repository: chú thích cho class giúp truy vấn dữ liệu database
 - @Service: chú thích cho class xử lý logic
 - @Controller: chú thích class làm việc với Request

# 10. Các Anotation


# 11. Lập trình hướng khía cạnh AOP và lập trình hướng đối tượng OOP

|  | AOP (Aspect Oriented Programming) | OOP (Object Oriented Programming) |
|---|---|---|
| Mô tả | Kiểu lập trình cho phép tách các module (chia nhỏ và dùng lại) | Là phương pháp lập trình dựa trên khái niệm về lớp và đối tượng |
