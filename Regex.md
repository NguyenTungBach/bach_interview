<img width="729" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/d116c9e2-576a-48fd-8430-e3a4107ca868">

# 1. Cấu trúc

<img width="418" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/b5a4c26f-accd-41ce-b943-ecefe4e479ae">

- pattern (trong 2 dấu //)
- flag (bên ngoài)

# 2.Flag:

| Ký tự | Ý nghĩa | Ví dụ |
| ------ | ------ | ------ |
| /g  | Tìm kiếm toàn bộ | Tìm toàn bộ chữ e  <img width="702" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/4c4f528a-13e9-406e-bf0c-76d871c19b6b"> |
| /i  | Tìm kiếm toàn bộ bỏ qua chữ hoa chữ thường | Tìm toàn bộ chữ e E <img width="719" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/f1fa9a46-ee1c-48e9-9911-ef75484ac6b8"> |
| /m  | Tìm kiếm trên nhiều dòng | Tìm số đầu từ 1->3 <img width="722" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/913ac4b5-21e7-4fd9-bd50-59d5fa73d923"> <img width="721" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/aa0ff428-0a03-4ff3-a1af-40f14f28ff93"> |

# 3.Pattern:
### 3.1: Nhóm ký hiệu assertions (tìm kiếm vị trí)

| Ký tự | Ý nghĩa | Ví dụ |
| ------ | ------ | ------ |
| ^ | Tìm ký tự đầu tiên của dòng | tìm chữ t đầu tiên **của dòng** <img width="647" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/761b8fb5-c021-4c46-b023-3cc96c401bbe"> |
| $ | Tìm ký tự kết thúc của dòng | Tìm chữ a cuối cùng **của dòng** <img width="648" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/70a1f83e-30aa-4ec3-a0f1-47c1a23b6e29"> |
| \b | Tìm kiếm ký tự nằm ở giữa từ và 1 dấu cách | Tìm chữ on với điều kiện trước nó là một dấu cách <img width="648" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/a10b0388-afc1-4427-9432-0d08efdf15a1">|

### 3.2: Nhóm character classes (danh sách tìm kiếm chữ và số)

| Ký tự | Ý nghĩa | Ví dụ |
| ------ | ------ | ------ |
| \d | tìm các số từ 0-9 | <p>Tìm tất cả số:</p> <img width="644" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/274ab53d-c7d9-4e0f-b91f-5c901683460d">  <p>Tìm tất cả ký tự số liền nhau:</p> <img width="646" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/14a69697-8430-4a03-a534-745de5185684"> <p>Tìm ký tự số liền nhau ở vị trí cuối cùng:</p> <img width="647" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/ff5bfca8-f9ba-4367-be0e-08c86a49f772"> |
| \w | Tìm ký tự la tinh và dấu gạch chân (A-Z a-z 0-9 _) | Tìm toàn bộ chữ la tinh <img width="677" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/ffd24441-0c9b-4ffd-a495-39b6846046ee"> |
| \s | Tìm dấu cách | Tìm toàn bộ dấu cách <img width="689" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/ddfc57a6-e8b2-464d-b47a-36f4e0219c66"> |
| \S | Tìm ký tự không phải dấu cách | Tìm ký tự không phải dấu cách <img width="805" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/64880fd7-d542-4a35-afaa-0bc5181619a9"> |
| + | Tìm ký tự lặp đi lặp lại ít nhất 1 lần | Tìm các số <img width="646" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/c17ae214-8f7c-49b8-8ae7-16c77c025560"> |
| . | Tìm bất kỳ ký tự trong văn bản | Tìm toàn bộ 2 ký tự kèm số 6 <img width="649" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/623fa385-2206-480f-b8dd-898a4f1caa1f"> |

### 3.3: Sets and  ranges (Tập hợp và Khoảng ký tự)

<img width="502" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/9c131b85-ef61-4d2c-925b-4d7d4bf30816">

#### 3.3.1: Sets (tập hợp)
VD1: tìm toàn bộ ký tự có chữ m,t,p,c

<img width="650" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/619dc0b6-ed9e-4c51-937c-e12d82e8f3ba">

VD2: tìm chữ có đuôi op và ký tự đằng trước có chữ m,t,p,c

<img width="652" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/d8a3485f-7932-43cd-bce2-ae52bc6370d3">

#### 3.3.2: Ranges (Khoảng ký tự)
VD1: tìm ký tự đầu # và các ký tự khoảng a-z 0-9 lặp 3 lần

<img width="647" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/7da1105a-38c7-42c2-b579-5cf86e55d104">

VD2: tìm các ký tự không nằm trong khoảng từ 1-5

<img width="650" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/0cb8d955-2eb8-4377-970e-beb124b1d11e">

### 3.4. Greedy Quantifiers (Nhóm định lượng x+ x*): giúp không phải lặp đi lặp lại ký tự nhiều lần

<img width="389" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/5946a64a-4fec-4ae9-aff9-78ae1fb0670a">

VD1: tìm những số lặp đi lặp lại 5 lần

<img width="647" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/c598730c-eac3-4484-9391-ed90441da1ea">

VD2: tìm những số lặp đi lặp lại khoảng 3-4 lần

<img width="485" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/39e3ca77-03a2-4967-b5a8-c43752582892">

VD3: tìm những số lặp đi lặp lại ít nhất 4 lần

<img width="527" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/2e439e41-e57d-4e50-bfca-f6001fa45a3f">

VD4: tìm một số theo sau đó có thể là 1 dãy các số 0 hoặc không có

<img width="462" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/65eaa6b8-6109-42e8-83cf-02f8e4dd9d6c">

VD5: tất cả colou(bất kỳ)r, với chữ **bất kỳ** có thể có hoặc không. Ví dụ ở đây chữ u có thể có hoặc không

<img width="646" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/20277cd1-cba9-4bcf-83d0-6f0914a47992">

### 3.5. Lazy Quantifiers (x+? x*?):

VD1: tìm những ký tự nằm trong dấu ""

<img width="650" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/3b852b39-cc1e-47c7-b550-6fb65cd78133">

### 3.6. Capturing groups (nhóm nhiều ký tự, lấy riêng tên): (?<name>x)

<img width="540" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/b836602d-96d8-41e8-947a-145b0464c7a2">

VD1: tìm những ký tự chữ go

<img width="647" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/aa81f584-4c99-467b-af40-4dfe64f844e4">

VD2: tìm tách lấy ra năm và tháng có đặt tên year, month

<img width="629" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/5a232210-ce18-4c1f-b0f1-7e05fbf688ce">

