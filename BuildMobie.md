# 1. build apk (android)
- clone link git cần tải
- (Nếu có) sửa link api vào các file có **https://**
  - until/appConfig.ts: sửa API_SERVER (lưu ý nhớ chữ /api)
   ![](https://res.cloudinary.com/dark-faith/image/upload/v1694143042/veho%20tutorial/build_change_api_server_1_x6z65h.png)

  - src/constants/config.ts:
  ![](https://res.cloudinary.com/dark-faith/image/upload/v1694143411/veho%20tutorial/build_change_api_server_2_rdvp5p.png)

- vào android studio (lưu ý chọn thư mục app)
  - Nhấn Buld/Generate Signed Bundle or APK -> Chọn APK 
  ![](https://res.cloudinary.com/dark-faith/image/upload/v1694400210/veho%20tutorial/build_change_api_server_4_d3ojjc.png)
  ![](https://res.cloudinary.com/dark-faith/image/upload/v1694400437/veho%20tutorial/build_change_api_server_APK_vwyv9k.png)
  - Key store path
    - Trường hợp đã tồn tại thì chọn Choose existing và nhập mật khẩu
    ![](https://res.cloudinary.com/dark-faith/image/upload/v1694400612/veho%20tutorial/build_change_api_server_5_qvmrbk.png)
    - Trường hợp chưa tồn tại thì chọn Create new và điền thông tin và nhập đúng mật khẩu vừa tạo
    ![](https://res.cloudinary.com/dark-faith/image/upload/v1694400002/veho%20tutorial/build_change_api_server_3_qgokqi.png)
  - Chọn release để tạo file apk
    ![](https://res.cloudinary.com/dark-faith/image/upload/v1694400877/veho%20tutorial/build_change_api_server_6_yeeisg.png)
  - File apk sau khi tạo xong sẽ hay được để ở **TÊN_PROJECT\android\app\release**
  ![](https://res.cloudinary.com/dark-faith/image/upload/v1694401109/veho%20tutorial/build_change_api_server_7_vlkwhl.png)
  
# 2. build ios (test flight)
- tạo new folder
- git clone project
- sửa lại tên project nếu cần (Lưu ý trường hợp này cần người giúp vì sửa tên toàn bộ file rất dễ lỗi)
  ![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1695022744/server_deploy/change%20all%20file%20ios%20and%20android%20%28warning%29.png)
  
- yarn install
- cd ios
- pod install: build ios
- Tạo bundle id trên test flight để định danh (Mỗi 1 app đều có 1 bundle id)
  - Vào browser, nhấn nút tạo với đường dẫn (nhớ đăng nhập) https://developer.apple.com/account/resources/identifiers/list
  ![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1695021562/server_deploy/create%20new%20bundle%201.png)

  - Chọn và tạo đúng như các bước dưới đây
  ![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1695021892/server_deploy/create%20new%20bundle%20id%202.png)
  ![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1695022011/server_deploy/create%20new%20bundle%20id%203.png)
  ![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1695022102/server_deploy/create%20new%20bundle%20id%204.1%20%28input%29.png)
  ![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1695022179/server_deploy/create%20new%20bundle%20id%204.2.png)
  ![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1695022247/server_deploy/create%20new%20bundle%20id%204.3.png)

  - Tạo app mới cho test flight **(Dùng bundle id)**
  ![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1695022352/server_deploy/create%20new%20app.png)

- Mở x code (để deploye lên test flight)
  - Tìm file ios/TÊN_FILE.xcworkspace 
  ![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1695020743/server_deploy/file%20build%20ios.png)
  - Vào browser với đường dẫn

- Sau khi tạo xong có thể add thành viên vào để đăng ký dùng thử app test flight
  ![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1695022528/server_deploy/create%20group%20test%20flight%205.1.png)
  ![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1695022598/server_deploy/add%20member%20group%20test%20flight%205.2.png)
  ![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1695022634/server_deploy/add%20member%20group%20test%20flight%205.3.png)
