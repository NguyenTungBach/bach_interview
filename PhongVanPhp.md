## 1. GET và POST
- GET là phương thức truyền tham số thông qua url. (Việc truyền dữ liệu bằng url sẽ bị giới hạn nên thường dùng để lấy dữ liệu về)
- POST là phương thức truyền tham số thông qua HTTP request body (Không giới hạn việc truyền dữ liệu nên thường dùng để gửi dữ liệu lên). Thực ra php là có bị giới 
vậy nên cần dùng ini_set('memory_limit', '-1');

## 2. Cookie và Session
- Cookie lưu trữ thông tin phía người dùng -> dễ sửa đổi do lưu phía trình duyệt ***(Clean sau khi hết thời gian)***
- Session lưu trữ thông tin phía server -> Khó sửa đổi do lưu trên server ***(Clean sau khi đóng trình duyệt)***

## 3. Localstorage, Sessionstorage và Cookie
- Localstorage lưu trữ vô thời hạn
- Sessionstorage được hủy sau khi đóng tab hoặc thoát trình duyệt
- Cookie được hủy sau khi hết hạn hoặc xóa bằng java script, php bằng hàm unset

## 3. Hằng trong PHP khác gì so với biến
- Biến thì chỉ cần dùng ký tự $ để gắn hoặc lấy giá trị.
- Hằng dùng hàm define() gắn giá trị và dùng constant() để lấy giá trị.

```sh
Cú pháp: define('Tên hằng', value);
```

Nếu 1 hằng được định nghĩa 2 lần thì chương trình vẫn chạy được bình thường tuy nhiên hằng chỉ có giá trị của lần định nghĩa đầu tiên

## 3. Mảng là gì?
- Là một biến chứa nhiều phần tử
- Mảng tuần tự: là mảng có key tự động tạo là chữ số tăng dần bắt đầu từ 0.
```sh
$phims = array(0 => "One Piece",
               1 => "Dragon Ball",
               2 => "Doremon",
               3 => "One-Punch Man",
               4 => "Naruto" );
```

- Mảng không tuần tự(mảng đa chiều): là mảng có key mà bạn phải tự định nghĩa bằng các ký tự chữ hoặc số, và key không được sắp xếp bất kỳ thứ tự nào.

```sh
$sinhVien = array("Hải" => "Nam", "Doanh" => "Nam", "Nhung" => "Nữ");
print_r($sinhVien);


Array ( [Hải] => Nam [Doanh] => Nam [Nhung] => Nữ )
```

- Mảng đa chiều: là mảng có chứa ít nhất một mảng khác trong nó.

```sh
$phims =array(
  "Hành động" => array("Jonh Wick", "Người vận chuyển", "Nhiệm vụ bất khả thi"),
  "Viễn tưởng" => array("Endgame", "Infinity War"),
  "Lãng mạn" => array("La La land"),
  "Kịch tính" => array("Tên trộm và cô chủ nhà")
);
```

# 4. Rest API là gì?
Là 1 giao thức tạo ra API. 
 - get -> lấy
 - post -> gửi
 - put sửa
 - delete -> xóa

# 5. RestFull API là gì?
Là giao thức định nghĩa ra các chuẩn giao thức viết API
 - get/products -> lấy tất cả product
 - get/products/{id} -> lấy product theo id
 - put/products/{id} -> sửa product
 - delete/products/{id} -> xóa product

# 6. & và && trong PHP
- & trả về 0 hoặc 1
- && trả về True và False

# 7. $$ trong PHP
- ví dụ 
```sh
$a = "hello";
$$a = 200;
```
Tương đương với việc tạo ra $hello = 200

# 7. Trait trong PHP
-  Hỗ trợ đa kế thừa

```sh
trait Database
{
    public function listUsers()
    {
        return "List users!";
    }
}

trait Authenticate
{
    public function authorize()
    {
        return "Authorized!";
    }
}

class Users
{
    use Database, Authenticate;

    public function __construct()
    {
        $this->authorize();
    }

    public function index()
    {
        $this->listUsers();
    }
}
```

# 8. ++ i Và i ++
-  ++i tính luôn trên giá trị ban đầu
-  i++ tạo ra bản copy của giá trị ban đầu. nên nếu in ra luôn thì hiện nó vẫn thế

```sh
// Nếu in ra luôn
++i = 1
// Nếu in ra luôn
i++ = 0 
```

# 9. PHP là đơn luồng hay đa luồng
- PHP là đơn luồng, nghĩa là chỉ thực hiện một tác vụ một thời điểm (vì khồng có tính năng đa luồng). Khác Java là ngôn ngữ lâp trình đa luồng vì Java hỗ trợ thực thi nhiều luồng

# 10. PHP là thừa kế đơn hay thừa kế đa
- PHP là thừa kế đơn do chỉ extend được từ 1 lớp khác

# 11. include và requied
Cả 2 đều dùng để import một file PHP vào file hiện tại. Mục đích để phân tách trang, thuận lợi cho việc chỉnh sửa nhiều trang (giồng laravel chia tách file @include và @yield)
- include: code sẽ tiếp tục được thục thi, cho dù file đó có tồn tại hay không
- requied: code sẽ không được thục thi, nếu file đó không tồn tại
