### 1 .Spring là gi?
- Spring là framework dựa trên ngôn ngữ java để xây dựng các ngôn ngữ phần mềm.
- Có những ưu điểm:
    - Tạo sẵn server test. Thay vì mình phải tìm cách cài tomcat để chạy thử server thì spring đã cung cấp sẵn
    - Hỗ trợ cấu hình tự động (file application.properties)
    - Cung cấp nhiều framework có sẵn để làm việc như 
        - Spring Data JPA: Hỗ trợ làm việc database
        - Spring Sercurity: Hỗ trợ làm việc với xác thực và phân quyền
        - Spring Boot: Cung cấp các cấu hình sẵn mặc đinh hay tích hợp các công nghệ của các ứng dụng Spring

### 2 . ORM là gì?
ORM là một framework trong việc ánh xạ đối tượng với database

### 3 .JPA là gi?
- Là đặc tả của ORM trong việc ánh xạ đối tượng với database

### 4 .Hibernate là gi?
- Là framework của ORM trong việc ánh xạ đối tượng với database
    - Ưu điểm:
        - Có HQL: giúp việc thay đổi database sẽ không phải lo việc thay đổi code
        - Có thể mapping với object để tạo bảng database

### 5 .Spring data Jpa là gi?
- Là dependency ***(Dependency (phụ thuộc) là một thành phần (modul) hoặc thư viện cung cấp các tính năng cho chương trình hoặc ứng dụng đó)*** của Spring boot, cung cấp các tính năng giảm thiểu code. Như
    - Cung cấp các hàm truy vấn tự động giúp hỗ trợ đa nền tảng nhiều database khác nhau. Khi thay đổi database sẽ không phải lo việc thay đổi code
    - Cung cấp các hàm truy vấn có sẵn để làm việc với database như save(), findById(), findAll().

### 6 .Native là gi?
- Native query là query thuần ko chỉ đến các object entities. Lý do viết thuần là vì có một số câu lệnh, một số hàm mà chỉ trên chính database đó mới có

### 7 .Authentication (xác thực) và Authorization (phân quyền) là gi?
- Xác thực là bạn là ai, phân quyền là bạn được quyền gì

### 8 .Các bước xử lý bug?
- B1 tái hiện bug
- B2 debug từng break point (điểm chương trình)
