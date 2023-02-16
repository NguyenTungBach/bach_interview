## 1. Cách sử dụng VueJS với các API: Hỏi về cách sử dụng VueJS để gọi và xử lý dữ liệu từ các API
...

## 2. VueJS Reactive Properties: Hỏi về cách sử dụng các thuộc tính reactive trong VueJS và cách nó liên quan đến việc cập nhật giao diện.
- ref: nếu muốn gọi ra thì trong file script phải .value
- reactive: dành cho các body gọi trực tiếp, không cần phải .value

## 3. VueJS Lifecycle Methods: Hỏi về các phương thức của VueJS lifecycle và cách sử dụng chúng để xử lý logic trong quá trình tạo và hủy của một component.
- onBeforeMounted: trước khi load trang
- onMounted: sau onBeforeMounted (tức là DOM đc sinh ra rồi)
- onUnMounted: khi DOM bị hủy (VD: khi component cũ chuyển sang component mới. Thì quá trình component cũ bị hủy thì là onUnMounted)
- onBeforeUnMounted: trước khi DOM bị hủy
- onBeforeUpdate: trước khi có giá trị gì thay đổi trong trang (VD: nhấn nút)

## 4. VueJS Mixins: Hỏi về cách sử dụng mixins trong VueJS để tái sử dụng code và chia sẻ logic giữa các component.
- Là những component có thể dùng lại được (ví dụ select, table, layout)

## 5. VueJS Custom Directives: Hỏi về cách tạo và sử dụng custom directives trong VueJS để xử lý logic đặc biệt.
- Tạo một sự kiện riêng

## 6. VueJS Transitions and Animations: Hỏi về cách sử dụng các transitions và animations trong VueJS để tạo hiệu ứng cho giao diện.
- Tạo hiệu ứng cho giao diện

## 7 .VueJS Server-side Rendering (SSR): Hỏi về việc sử dụng VueJS cho server-side rendering (SSR) và cách nó ưu điểm so với việc render trên client-side.
- Ưu điểm: có thể SEO đc. Khi render phía server
- VueJS Server-side Rendering: Thuận tiện cho SEO (Chú trọng đọc các thẻ trong HTML). Bot của google có thể đọc hết tất cả các thẻ vì SSR đã render ra HTML
- VueJS client-side : Khi render phía client. Đóng gói vào 1 file script, Boot của google chỉ nhìn được file script thôi.

## 8 .Computed và watch
- computed lắng nghe trước khi dữ liệu đã render, computed có thể là 1 biến. Khi lưu giá thay đổi thì sẽ lưu vào bộ nhớ cache ở thời điểm đã render ra, không gán đc biến ngay từ đầu.
- watch lắng nghe sự thay đổi sau khi dữ liệu đã render, chỉ là hàm lắng nghe sự thay đổi của biến tại 1 component
