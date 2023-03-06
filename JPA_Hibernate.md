### 1. JPA là gì?
- JPA là công nghệ của ORM. Dùng để ánh xạ dữ liệu đối tượng với database. Và JPA là một tiêu chuẩn
- Sử dụng thư viện javax.persistence để định nghĩa ra các Annotation và API để làm việc với database. Đặc điểm nhận dạng là EntityManager

### 2. Hibernate là gì?
- Hibernate là công nghệ của ORM. Dùng để ánh xạ dữ liệu đối tượng với database
- Sử dụng thư viện chính là org.hibernate còn các thư viện khác bao gồm:
    - javax.persistence: Chứa các Annotation và API của tiêu chuẩn JPA để định nghĩa 
    - org.hibernate: Chứa các gói chính của hibernate, đặc điểm nhận dạng là dùng Session và SessionFactory để truy vấn
    - antlr: 
    - javassist: 
    - commons-logging: Thư viện này được Hibernate sử dụng để ghi lại các thông tin cần thiết trong quá trình sử dụng Hibernate

### 3. Spring Data JPA là gì?
- Spring Data JPA là framework của Spring boot giúp giảm thiểu các đoạn code.
  - Spring Data JPA sử dụng các phương thức truy vấn tạo tự động để truy vấn. Nhờ các phương thức tạo tự động nên nó có thể hỗ trợ đa nền tảng với database khác nhau
  - Spring Data JPA cung cấp một số phương thức có sẵn để thao tác với cơ sở dữ liệu. Như save(), findById(), findAll()
  
