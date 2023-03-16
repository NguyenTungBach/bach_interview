### 1 .Spring là gi?
- Spring là framework của java giúp lập trình viên giúp đơn giản hóa việc code.
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

### 6 .Native query (một tính năng của JPA) là gi?
- Native query là query thuần ko chỉ đến các object entities. Lý do viết thuần là vì có một số câu lệnh, một số hàm mà chỉ trên chính database đó mới có

### 7 . Spring data Jpa và Hibernate?
- đều ko dùng đc các chức năng đặc trưng cảu db nên vẫn cần phải viết thuần cho một số trường hợp

| | Spring data JPA | Hibernate |
| ------ | ------ | ------ |
| Định nghĩa  | là dependencies của spring | Là framework của ORM trong việc ánh xạ đối tượng với database |
| Chứa  | chứa hibernate | là một tích hợp nằm trong Spring data Jpa |
| Tính năng đặc trưng  | Cung cấp các hàm truy vấn tự động giúp hỗ trợ đa nền tảng nhiều database khác nhau và các hàm truy vấn có sẵn để làm việc với database như save(), findById(), findAll(). | Giúp thay vì làm việc với database thì làm việc với đối tượng và giúp ánh xạ đối tượng với database để tạo bảng |

### 8 . JDBC và Hibernate?
| | JDBC | Hibernate |
| ------ | ------ | ------ |
| Định nghĩa  | là thư viện của java giúp làm việc với database | Là framework của ORM trong việc ánh xạ đối tượng với database |
| Tạo bảng  | tạo bảng thủ công | tự động mapping object vs table |
| truy vấn  | truy vấn qua database | truy vấn qua object |

### 8 .Authentication (xác thực) và Authorization (phân quyền) là gi?
- Xác thực là bạn là ai, phân quyền là bạn được quyền gì

### 9 .Các bước xử lý bug?
- B1 tái hiện bug
- B2 debug từng break point (điểm chương trình)
