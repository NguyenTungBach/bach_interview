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
  
