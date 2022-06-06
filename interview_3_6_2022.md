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



