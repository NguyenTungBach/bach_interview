#Tại sao java là nn độc lập nền tảng


jvm giúp cho java chạy tốt các nền tảng khác nhau
-Tại sao lại dùng bản jdk 8 
Là vì tính ổn định cần khi phát triển sản phẩm
-Tính năng của jdk 8
Lamda, tream, colection api, for each, colcurency
-Overiding
LÀ thể hiện của đa hình cùng phương thức thể hiện theo các cách khác nhau
Cùng method, tham số, 
-Hit, stack trong java
hit(lỗi: out of memory: tràn bộ nhớ): chứa các ob 
stack(stack overflow): nhỏ hơn hit, thường lưu những biến nguyên thủy
-Luồng
Khi cần chương trình chạy nhanh hơn
-@transactional
Khi 2 thằng gọi đến nhau thì nó sẽ chỉ là 1(defaul là v). Nếu muốn tách ra thì sẽ có funcion để tách
Khi tương tác vs db nếu lỗi giữa chùng thì sẽ rollback lại
VD: Khi insert 100 nhưng nếu đến 10 lỗi thì sẽ quay lại từ đầu(hoặc vào all hoặc ko vào)
-Sự khác nhau giữa == và equal
==: phải là object, ko bị gặp lỗi null queter exeption, so sánh địa chỉ
equal: so sánh nội dung
-Interface
Tính bao quát
Dễ bảo trì
-Tham chiếu và tham trị*
Tham chiếu: truyền theo tham chiếu
Tham trị: truyền theo giá trị
-Kdl enum
Giới hạn lựa chọn(ltvien)
-Reflection trong java(Ko còn vì dùng framework)(autowired)(nguy hiểm, gây những lỗi ko xác định)
Vd: khi extend JpaRepos có thể truyền vào dù là cus, std
Là một cách nhìn lại tất cả tt trong class
Nhìn sâu vào class mà ko cần bt là class j
-Generate type
Là tham số hóa kdl, 
vd về array list
-Spring profile
Db: 
Spring: 
-Var aguiment
... có thể xử lý 1 hay nhiều chuỗi cx đc
Có thể cho không giới hạn vào
-fail-fast và fail-safe
khi sửa mà sinh ra lỗi thì là lỗi ff fs
Khi làm việc với các phần tử có thể xảy ra lỗi
-Builer design pattern
Thay vì làm việc trên 1 dòng lệnh thì sẽ làm trên nhiều dòng
-Singertern design pattern
static, get instant
đảm bảo ob đấy là duy nhất trong pr
-List và mảng
-Hashset
Put vào đó 2 int hay 2 string thì nó sẽ phân biệt đc là 1, nếu put vào 2 đối tg thì sẽ là 2
Class dùng thì phải compare to, vd 2 id giống nhau thì là 1 thg ob
Phải làm cho hashset phân biệt thế nào là 2 ob khác nhau














