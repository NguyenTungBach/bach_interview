# 1. Một số lưu ý
## 1.1 Vì đã có sẵn trong cấu hình ios với detox nên sẽ phải bỏ qua một số bước cấu hình detox. Dưới đây là một số file cần thay đổi
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

## 2.2 build.gradle
   ### 2.2.1: Điền version
   - 2.2.1.1: Kiểm tra version và kotlinVersion

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1703650870/detox/detox_android_build.gradle_check_version_build_and_kotlin.png)

   - 2.2.1.2: Điền thông tin dưới đây

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1703650550/detox/detox_android_build.gradle_buildscript%20%281%29.png)

   ### 2.2.2: Nhập các thư viện android/build.gradle
```sh
 buildscript {
   ext {
     ....
      kotlinVersion = 'X.Y.Z' // (2)
   }
…
repositories {
       …
+        maven {
+            url ("$rootDir/../node_modules/detox/Detox-android")
+        }
    }
 …
   dependencies {
+    classpath("org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlinVersion") // (3)
 …
 allprojects {
   repositories {
     …
     google()
+    maven { // (4)
+      url("$rootDir/../node_modules/detox/Detox-android")
+    }
     maven { url 'https://www.jitpack.io' }
   }
 }
```

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1703650550/detox/detox_android_build.gradle_buildscript%20%281%29.png)
![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1703651618/detox/detox_android_build.gradle_dependencies_and_allprojects%20%282%29.png)

   ### 2.2.3: Nhập các thư viện android/app/build.gradle
```sh
 …

 android {
   …
   defaultConfig {
     …
     versionCode 1
     versionName "1.0"
+    testBuildType System.getProperty('testBuildType', 'debug')
+    testInstrumentationRunner 'androidx.test.runner.AndroidJUnitRunner'
   …
   buildTypes {
     release {
       minifyEnabled true
       proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
+      proguardFile "${rootProject.projectDir}/../node_modules/detox/android/detox/proguard-rules-app.pro"

       signingConfig signingConfigs.release
     }
   }
   …

 dependencies {
+  androidTestImplementation('com.wix:detox:+')
+  implementation 'androidx.appcompat:appcompat:1.1.0'
   implementation fileTree(dir: "libs", include: ["*.jar"])
```

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1703652057/detox/detox_android_app_build.gradle_android%20%282%29.png)
![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1703651940/detox/detox_android_app_build.gradle_buildTypes%20%281%29.png)
![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1703652165/detox/detox_android_app_build.gradle_dependencies%20%283%29.png)

   ### 2.2.4: Tạo file khởi động chạy test android cho detox
- android/app/src/androidTest/java/com/<Tên.package>/DetoxTest.java

```sh
// Replace "com.example" here and below with your app's package name from the top of MainActivity.java
package <Tên.package ví dụ com.atmtcmobile>;

import com.wix.detox.Detox;
import com.wix.detox.config.DetoxConfig;

import org.junit.Rule;
import org.junit.Test;
import org.junit.runner.RunWith;

import androidx.test.ext.junit.runners.AndroidJUnit4;
import androidx.test.filters.LargeTest;
import androidx.test.rule.ActivityTestRule;

@RunWith(AndroidJUnit4.class)
@LargeTest
public class DetoxTest {
    // Replace 'MainActivity' with the value of android:name entry in
    // <activity> in AndroidManifest.xml
    @Rule
    public ActivityTestRule<MainActivity> mActivityRule = new ActivityTestRule<>(MainActivity.class, false, false);

    @Test
    public void runDetoxTests() {
        // This is optional - in case you've decided to integrate TestButler
        // See https://github.com/wix/Detox/blob/master/docs/Introduction.Android.md#8-test-butler-support-optional
        // TestButlerProbe.assertReadyIfInstalled();

        DetoxConfig detoxConfig = new DetoxConfig();
        detoxConfig.idlePolicyConfig.masterTimeoutSec = 90;
        detoxConfig.idlePolicyConfig.idleResourceTimeoutSec = 60;
        detoxConfig.rnContextLoadTimeoutSec = (BuildConfig.DEBUG ? 180 : 60);

        Detox.runTests(mActivityRule, detoxConfig);
    }
}
```


![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1703652458/detox/detox_android_detoxtest.java.png)

### 2.2.5: setting.gradle
- android/setting.gradle

```sh
...
include ':detox'
project(':detox').projectDir = new File(rootProject.projectDir, '../node_modules/detox/android/detox')
...
```

![](https://res.cloudinary.com/do5mcnq9w/image/upload/v1703652974/detox/download_kelegn.png)

# 3. Chạy hai lệnh để build
- npx detox build -c android.emu.debug: cấu hình detox (tìm android.emu.debug ở trong file detoxrc.js)
- npx detox test -c android.emu.debug TênFile.test.ts: chạy 1 IT cụ cụ thể
