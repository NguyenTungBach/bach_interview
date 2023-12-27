# 1. Một số lưu ý
## 1.1 Vì đã có sẵn trong cấu hình ios với detox nên sẽ phải bỏ qua một số bước cấu hình detox. Dưới đây là những file cần thay đổi
   ![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1703649075/detox/detox_android_all_file_change.png)

## 1.2 Lưu ý nếu có một số file bị sai đường dẫn thì hãy cd vào android sửa lại và chạy lệnh 
  - ./gradlew clean: xóa hết cấu hình android
  - ./gradlew assembleRelease: build lại android
  - npx detox build -c android.emu.debug (nếu đẫ cấu hình detox): build lại cấu hình chạy test detox
  
![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1703647856/detox/download_x0fiaq.png)
  
## 1.3 Khi chạy test detox giả lập có thể không nhận cổng cho máy ảo nên phải thêm vào hai lệnh này cùng lúc khi chạy test
  - adb reverse tcp:8081 tcp:8081: để máy ảo nhận cổng port 8081
  - react-native start: chạy react-native

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1703648550/detox/detox_android_run_test_example.png)
![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1703648690/detox/detox_adb_set_port.png)
  
   
# 2. Cấu hình android
## 2.1 .detoxrc.js
  - Đây là nơi cấu hình chạy android giả lập và câu lệnh buid
    - devices: các thiết bị giả lập
    - apps: chứa các file và câu lệnh giả lập
    - configurations: cấu hình tổng để chạy lệnh test cho app nào thiết bị gì
  - Ở đây tôi chỉ làm phần liên quan đến cấu hình mình cần 

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1703649973/detox/detox_android_detoxrc_emulator.png)
![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1703650089/detox/detox_android_detoxrc_app.png)
![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1703650170/detox/detox_android_detoxrc_configurations.png)
