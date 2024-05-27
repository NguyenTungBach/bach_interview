# Sơ qua các bước
- B1: Cấu hình đăng ký slack
- B2: Tạo laravel và code
- B3: Tạo server ảo Ngrok giúp kết nối giữa localhost và internet

## B1: Cấu hình đăng ký slack
### 1.1 tạo tài khoản slack (đăng ký bằng google cho nhanh)
- Sau khi đăng nhập vào
<img width="518" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/85699b30-98e7-4cac-a84f-96cfbdcce38f">

### 1.2 tạo tài workspace và channel
- Sau khi đăng nhập thành công nhấn **create workspace** để tạo một workspace
<img width="500" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/52eb0220-054d-44f6-b22c-09859eac4bc6">

- Điền email để xác thực
<img width="518" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/93162fb9-265f-4bad-8753-baddd8b67f04">

- Điền tên workspace tạo
<img width="1280" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/ad0f0abf-cabc-469b-ac0b-22891d748cf1">
<img width="933" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/c9baf865-46b4-475b-8d4e-61ca4da1defa">

- Điền tên của mình và ảnh đại diện
<img width="998" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/b9084acf-2bbc-4788-87fb-623c7acf34d9">

- Điền tên thành viên được thêm vào (có thể skip)
<img width="1036" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/2563d559-9d2c-4e24-831c-7e665327a941">

- Điền tên channel
<img width="1049" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/a6e322cb-84b3-4c05-a6a6-c62bf79ec43b">

- Sau khi hoàn thành chọn **Start with free**
<img width="1018" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/858438d5-92fd-401a-85d3-5e19890d3c2b">

<img width="1237" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/ac1bf60f-7678-4042-b9ba-5ff719da69b8">

### 1.3 Cấu hình slack để tạo kết nối slack laravel
#### 1.3.1 tạo app
- Vào [slack api](https://api.slack.com/apps)
- Nhấn Create New App -> chọn From scatch
<img width="1261" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/3ba803e6-ce5b-42e4-912d-25535a41fd38">
<img width="1277" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/56660897-8043-4dd8-9b4a-92fd0c011bbf">

- Đặt tên cho app name và chọn workspace đã tạo
<img width="1280" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/a9e6d916-9ac7-4ee9-9906-e18f29d20123">

- Sau khi hoàn thành
<img width="1280" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/78f8a9e9-ed32-4230-aa6d-2fca4d3c7fa8">

#### 1.3.2 Tạo Webhooks
- Kích hoạt Webhooks
<img width="1268" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/aecec31b-abef-4f30-a408-8d1c66ff49ef">
<img width="1277" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/5c11341b-e02e-461b-97aa-0101d30ae8df">

- Tạo Webhooks (nhấn add new Webhooks)
<img width="833" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/e48004e2-681a-473a-ba58-613a9adca01c">

- Chọn vào channel đã tạo và **allow**
<img width="1280" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/36bdc077-95b4-4e86-8749-1f0d39332692">
<img width="1232" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/915a06e4-9a7a-4b99-b7ce-be8e47e8694b">

- Sau khi hoàn thành Webhooks và Token đều cùng được tạo (Xem trong Install App)
<img width="1270" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/c7c1f7e2-b754-4219-815e-0efc29c71583">
<img width="1278" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/1ccde7ad-8d71-4b41-b076-136ad5e80d05">
<img width="914" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/f3244403-e8fd-4979-a23b-88542bea895d">


## B2: Tạo laravel mới và code
### 2.1 Cài đặt
- composer require laravel/slack-notification-channel
<img width="1240" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/16ed15d1-162c-4b0f-a34b-e3f0c0b591d8">

### 2.2 Cấu hình .env
#### 2.2.1 Cập nhật trong `services.php` thêm `slack`
```
'slack' => [
    'notifications' => [
        'channel' => env('SLACK_BOT_USER_DEFAULT_CHANNEL'),
        'webhook_url' => env('SLACK_WEBHOOK_URL'),
    ],
]
```

<img width="1242" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/473fa168-7263-48cb-8b4c-512b909e85a6">

#### 2.2.2 Cấu hình .env
- Copy láy thông số Webhooks dán vào `SLACK_WEBHOOK_URL`
<img width="1277" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/e7c402bb-29a2-48ef-a14a-276d939a98c6">

- Copy láy thông số Channel ID dán vào `SLACK_BOT_USER_DEFAULT_CHANNEL`
<img width="907" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/a62006b9-e924-4278-9be4-e85a7c4ea55e">
<img width="923" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/00b41f46-667f-4ace-a149-035e91890331">

```
SLACK_BOT_USER_DEFAULT_CHANNEL=C068VPUB2LT
SLACK_WEBHOOK_URL="https://hooks.slack.com/services/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"
```
<img width="1259" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/0e5ea668-a1b4-4958-9f99-cd5895de1c29">

- Chạy xóa cache cấu hình: php artisan optimize

#### 2.2.3 Code 
- Tạo Notification: php artisan make:notification SlackNotification
<img width="1240" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/00bcc8f2-ef45-43fd-8a23-11a7eba933a7">

- Cập nhật file `SlackNotification.php` (Lưu ý hàm via phải đúng với cấu hình trong `services.php`)
```
<?php

namespace App\Notifications;

use Illuminate\Notifications\Messages\SlackMessage;
use Illuminate\Notifications\Notification;

class SlackNotification extends Notification
{
    protected $message;

    /**
     * Create a new notification instance.
     *
     * @return void
     */
    public function __construct($message)
    {
        $this->message = $message;
    }

    /**
     * Get the notification's delivery channels.
     *
     * @param  mixed  $notifiable
     * @return array
     */
    public function via($notifiable)
    {
        return ['slack'];
    }

    public function toSlack($notifiable)
    {
        $slackMessage = (new SlackMessage())
            ->content($this->message);

        return $slackMessage;
    }
}
```

- Cập nhật và test trong `api.php` (Ở đây viết luôn logic)
```
Route::post('/bach/send', function (Request $request) {
    // Test slack by packet slack-notification-channel
    $message = $request->input('message');

    Notification::route('slack', config('services.slack.notifications.webhook_url'))
        ->notify(new SlackNotification($message));

    return response()->json(['status' => 'Message sent to Slack']);
});
```
<img width="1252" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/c7c453b0-733d-4b26-948f-cc193c29ce5e">

## B3: Test message
- Lưu ý trường hợp muốn chỉ định tên cụ thể cần copy member ID và cấu trúc sẽ thế này `<@Memeber_ID>`
<img width="908" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/316836c0-ef1c-425d-91da-b674b7a5d92f">
<img width="959" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/a7e605db-f8c0-4555-b701-0768a78ba703">
<img width="910" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/cde0cc43-44de-45fe-903d-302419739c0f">
<img width="913" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/7bb9efca-f96f-41a2-aff7-90d2e10f4dd6">

- Message test: `veho360 part 1 <@U07572LSWAF>`
<img width="677" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/daf73d03-4340-4c9a-ae98-fe752d99a58e">

- Sau khi hoàn thành
<img width="689" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/f86d47b2-fd68-4c3c-a81b-eb597e1d14ba">



