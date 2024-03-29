## 1. Event và Listen và Queue
- Event là thằng tạo sự kiện. Với các tham số truyền vào
- Listen là thằng lắng nghe sự kiện, nhận các tham số truyền vào để thực hiện một hành động nào đó
- Vì trong laravel không có khái niệm về đa luồng nên Queue là một trong những được tạo ra để xử lý đa luồng

## 2. GET và POST
- GET là phương thức truyền tham số thông qua url. (Việc truyền dữ liệu bằng url sẽ bị giới hạn nên thường dùng để lấy dữ liệu về)
- POST là phương thức truyền tham số thông qua HTTP request body (Không giới hạn việc truyền dữ liệu nên thường dùng để gửi dữ liệu lên)

## 3. Cookie và Session
- Cookie lưu trữ thông tin phía người dùng -> dễ sửa đổi do lưu phía trình duyệt ***(Clean sau khi hết thời gian)***
- Session lưu trữ thông tin phía server -> Khó sửa đổi do lưu trên server ***(Clean sau khi đóng trình duyệt)***

## 4. Localstorage, Sessionstorage và Cookie
- Localstorage lưu trữ vô thời hạn
- Sessionstorage được hủy sau khi đóng tab hoặc thoát trình duyệt
- Cookie được hủy sau khi hết hạn hoặc xóa bằng java script, php bằng hàm unset

## 5. Request lifecycle trong laravel
- Configuration: cấu hình các framework trong laravel, các Service Providers
- Service Provider: để cấu hình và đăng ký khởi tạo các thành phần của ứng dụng, **(khởi tạo thông qua hàm register() để truyền vào service container, sau khi khởi tạo xong sẽ đến boot() để thực hiện việc gì đó như Observe partten lắng nghe sau khi sự kiện thêm sửa xóa thực hiện)**
- Route Dispatch: Tìm đến route
- Middleware: Lọc request **(trong này có Handle exception)**
- Controller: Xử lý request và các logic. Có thể trả về view hoặc Response luôn
- View: Nếu controller trả về view thì laravel sẽ render view đó trả về cho client
- Response: trả về kết quả response về cho client

## 6. CSRF (Giả dạng request từ webside khác)
- Là cách thức tấn công bằng cách giả dạng request từ webside khác
- VD: Hacker tạo 1 trang web với form có link POST của mình. Người dùng vô tình click vào đường link của trang web đó (kèm theo Cookie của người dùng) -> Hacker có thể truy cập vào đường link không mong muốn trên trang web mà vẫn trên danh nghĩa người dùng

## 7. CSRF Token
- Dùng để định danh
- Mỗi form đều chứa 1 token ẩn phía server gắn vào. Server sẽ so sánh 2 token đó có giống với token server gừi không

## 8. Cách query trong Laravel
- Query builder tương tác với DB
```sh
$users = DB::table('users')->where('status', 1)->get();
```

- Eloquent tương tác với model
```sh
$users = User::where('status', 1)->get();
```

## 9. Middleware  trong Laravel
- Là cơ chế lọc request. Thường dùng để kiểm tra đăng nhập

## 10. Service Provider trong Laravel
- Là trung tâm của việc khởi tạo tất cả ứng dụng trong laravel. Các package nào mà cài đặt qua composer cũng đều phải khai báo trong Service Provider

## 11. Service Container trong Laravel
- Dùng để quản lý các đối tượng và phụ thuộc (như IOC Container trong Spring boot)

## 12. Binding và Singleton trong Laravel
Cả 2 đều sử dụng để đăng ký và quản lý đối tượng
- Binding: được sử dụng để đăng ký các đối tượng và cung cấp chúng cho ứng dụng khi cần thiết. Khởi tạo mỗi lần gọi đến
- Singleton: được sử dụng để đăng ký các đối tượng và cung cấp chúng cho ứng dụng khi cần thiết. Chỉ khởi tạo một lần

## 13. Các design pattern trong Laravel
- Service Container: quản lý và khỏi tạo các đối tượng và các phụ thuộc
- DI(Dependency Injection): là kỹ thuật lập trình dùng để tiêm vào các phụ thuộc. Các class không giao tiếp với nhau bằng lớp triển khai mà bằng lớp trừu tượng
- Repository Pattern: giảm việc lặp code truy vấn với các cơ sở dữ liệu
- Observer Pattern: Lắng nghe sự kiện thêm sửa xóa của 1 model để thực hiện 1 hành động nào đó
- Strategy Pattern: Giải thích cho việc mình sẽ sử dụng tính năng nào. Cái này DI cũng đã thể hiện rõ. Ngày hôm nay tôi dùng tính năng nhà việt nam, ngày hôm kia tôi dùng dùng tính năng nhà nhật

## 14. Constructor trong laravel
- Thường dùng để tiêm sự phụ thuộc. Tức là thay vì mình phải tạo ra một đối tượng và quản lý chúng thì sẽ thông qua 1 thằng khởi tạo và quản lý hộ mình, cụ thể ở đây là đăng ký chúng trong Service Provide. Mục đích ở đây là để mình dùng lại nhiều lần và có thể thay đổi đối tượng mà không ảnh hưởng đến các tính năng
  - B1: Tạo một interface để định nghĩa ra các tính năng cần có
  - B2: Tạo một lớp Service hoặc Repository implement từ interface đó **(tại đây sẽ tiêm phụ thuộc vào constructor với Repository thì mình sẽ tiêm phụ thuộc với lớp model cần tương tác Datasbe, với Service thì mình sẽ tiêm phụ thuộc với Repository với Controller là service)**
  - B3: Tạo một Service Provide để đăng ký ràng buộc giữa các Interface và Class 
  - B4: Khi một class sử dụng thì nó không còn cần tương tác với class triển khai (Service hoặc Repository) mà thông qua các lớp trừu tượng là Service Provide

## 15. Model - View - Controler trong laravel
- Model: Tương tác dữ liệu với database để lấy dữ liệu về cho controller
- View: Hiển thị dữ liệu
- Controller: Lấy yêu cầu từ người dùng và gửi qua model để lấy dữ liệu và show ra view

Còn đúng hơn sẽ phải làm thêm cái này để tránh controller phải xử lý logic
- Model: Định nghĩa ra các thuộc tính trong database
- Service hoặc Repository: Để xử lý các logic nghiệp vụ từ model như các lệnh truy vấn phức tạp như đăng nhập đăng ký, thanh toán, tính toán, thống kê, mảng dữ liệu truy vấn về thông qua Repository **(với Service)** và lọc sửa thêm xóa với **(với Repository)**
- Controller: Nhận yêu cầu từ Request người dùng rồi gửi cho Service hoặc Repository để xử lý logic và show ra view
- View: Hiển thị dữ liệu

***Trong cách trên có thể tạo thêm các lớp Helper dùng để tạo ra các hàm logic dùng chung (ví dụ: hàm xử lý định dạng ngày tháng, xử lý chuỗi, mã hóa, tạo chuỗi ngãu nhiên,...)***

## 16. Quan hệ trong laravel
- $this->belongsTo(Tên lớp bảng phụ, khóa ngoại của bảng chính, khóa chính của bảng phụ): thuộc về một bảng nào;
```sh
class BlogFarm extends Model{
  protected $fillable = ['title','farm_id','url','thumbnail','description'];
    use HasFactory;
    public function farm():BelongsTo
    {
        return $this->belongsTo(Farm::class,'farm_id','id');
    }
}
```
***(Hiểu trên như câu lệnh SQL sau From BlogFarm JOIN Farm ON BlogFarm.farm_id = Farm.id )***

- $this->hasMany(Tên lớp bảng phụ, khóa ngoại của bảng phụ, khóa chính của bảng chính): Sở hữu nhiều với bảng nào;
```sh
class Farm extends Model{
  use HasFactory;
  protected $fillable = ['name', 'address', 'email', 'address', 'phone','thumbnail','description','created_at','updated_at','deleted_at'];

  public function products(): HasMany
  {
      return $this->hasMany(Product::class,'farm_id','id');
  }
}
```
***(Hiểu trên như câu lệnh SQL sau From Farm JOIN Prodcuct ON Prodcut.farm_id = Farm.id )***

- $this->belongsToMany(Tên lớp bảng phụ, tên bảng trung gian, khóa ngoại của bảng chính trong bảng trung gian, khóa ngoại bảng phụ trong bảng trung gian): quan hệ nhiều nhiều giữa hai bảng;
```sh
class Order extends Model
{
    public $timestamps = false;
    use HasFactory;

    // 1 order thuộc về nhiều product, (n - 1)
    public function products() : BelongsToMany
    {

        // sử dụng bảng OrderDetail làm trung gian để tìm kiếm product
        return $this->belongsToMany(Product::class,'order_details', 'order_id', 'product_id');
    }
```
