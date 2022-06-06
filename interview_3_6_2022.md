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

- heap(lỗi: out of memory: tràn bộ nhớ): chứa các kiểu dữ liệu **obj**  
- stack(stack overflow): nhỏ hơn heap, thường lưu kiểu dữ liệu nguyên thủy

### 6.Luồng

- Khi cần chương trình chạy nhanh hơn

### 7.@transactional

- Khi 2 thằng gọi đến nhau thì nó sẽ chỉ là 1(defaul là v). Nếu muốn tách ra thì sẽ có funcion để tách
Khi tương tác vs db nếu lỗi giữa chùng thì sẽ rollback lại

**VD: Khi insert 100 nhưng nếu đến 10 lỗi thì sẽ quay lại từ đầu(hoặc vào all hoặc ko vào)**

### 8.Sự khác nhau giữa == và equal

- equal: so sánh nội dung
- ==: so sánh địa chỉ **(lưu ý phải là object, ko bị gặp lỗi null queter exeption)**

### 9.Lợi ích dùng Interface

- Tính bao quát
- Dễ bảo trì

### 10.Tham chiếu và tham trị

- Tham chiếu: truyền theo tham chiếu
- Tham trị: truyền theo giá trị

### 11.Kiểu dữ liệu Enum

- Giới hạn lựa chọn

### 12.Reflection trong java

- (Ko còn vì dùng framework)(autowired)(nguy hiểm, gây những lỗi ko xác định)
Vd: khi extend JpaRepos có thể truyền vào dù là cus, std
- Là một cách nhìn lại tất cả tt trong class
- Nhìn sâu vào class mà ko cần bt là class j

### 13.Generate type
- Là tham số hóa kiểu dữ liệu
**VD: array list **

### 14.Spring profile (Đang cần xem lại)
- Db:
- Spring: 
- Var aguiment: có thể xử lý 1 hay nhiều chuỗi cx đc
Có thể cho không giới hạn vào

### 15.fail-fast và fail-safe (Đang cần xem lại)
- khi sửa mà sinh ra lỗi thì là lỗi ff fs. Khi làm việc với các phần tử có thể xảy ra lỗi

### 16.Builer design pattern
- Thay vì làm việc trên 1 dòng lệnh thì sẽ làm trên nhiều dòng

### 17.Singertern design pattern
- static, get instant đảm bảo obj đấy là duy nhất trong pr

### 18.List và mảng
- List có thể mở rộng phần tử
- mảng cố định các phần tử

### 19.Hashset
- Put vào đó 2 int hay 2 string thì nó sẽ phân biệt đc là 1, nếu put vào 2 đối tg thì sẽ là 2
- Class dùng thì phải compare to, vd 2 id giống nhau thì là 1 thg ob
- Phải làm cho hashset phân biệt thế nào là 2 ob khác nhau

