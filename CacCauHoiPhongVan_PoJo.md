### 1. Pojo là gì?
- Là lớp được triển khai các đặc điểm cơ bản nhất trong java như  như các thuộc tính, getter/setter, constructor và các phương thức equals(), hashCode(), toString().

### 2. IOC và DI?
- IOC dựa trên nguyên tắc ***(nguyên tắc là yêu cầu)*** solid. Trong nguyên tắc có nguyên lý ***(lý thuyết)*** DIP.
- Nguyên lý DIP chỉ ra các class không giao tiếp với nhau thông qua lớp triển khai (lớp implement gì gì đó) mà thống qua lớp trừu tượng (các interface, abtract)
- Dựa trên nguyên lý đó IOC tạo ra IOC Container để quản lý sự phụ thuộc.
- Còn DI và IOC về bản chất nó giống nhau là để giảm sự phụ thuộc. DI là một trong những triển khai của IOC

### 3. Bean là gì?
- Là một đối tượng được quản lý bởi IOC Container

### 4. Các cách khởi tạo bean?
- Anotation (thường dùng)
- XML
- JAVA BASE

### 5. Các cách khởi tạo bean bằng anotaion?
- @Bean: đặt trên hàm, kết quả của hàm này sẽ được IOC quản lý và trả về kết quả đó
- @Component: chú thích trên class, là một khuôn mẫu chung cho bất kỳ thành phần nào do Spring quản lý
- @Repository: chú thích cho class giúp truy vấn dữ liệu database
- @Service: chú thích cho class xử lý logic
- @Controller: chú thích class làm việc với Request
