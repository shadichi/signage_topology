<div dir="rtl">

# Configs (dart-define) — Digital Signage

## هدف
تنظیمات سراسری اپ TV.   
در فلاتر معمولاً به‌جای `.env` از `--dart-define` استفاده می‌کنیم.

---

## کلیدهای پیکربندی (پیشنهادی)

| کلید         |  مقدار                                              | کاربرد                 |
|--------------|----------------------------------------------------------|-----------------------------|
| BASE_URL     | https://aparatchi.yektahoosh.com                         | آدرس Backend API            |
| CAPTURE_URL  | https://aparatchi.yektahoosh.com/api/v1/tvscreen/capture | آپلود اسکرین‌شات (Multipart)|
| MQTT_URL     | mqtt://mqtt1.yektahoosh.com:6000                         | بروکر MQTT                  |
| TOPIC_PREFIX | yektahoosh/ds                                            | پیشوند تاپیک‌ ها             |



---

## نمونه اجرا با dart-define

```bash
flutter run \
  --dart-define=BASE_URL=https://aparatchi.yektahoosh.com \
  --dart-define=CAPTURE_URL=https://aparatchi.yektahoosh.com/api/v1/tvscreen/capture \
  --dart-define=MQTT_URL=mqtt://mqtt1.yektahoosh.com:6000 \
  --dart-define=MQTT_USER=device_user \
  --dart-define=MQTT_PASS=SECRET \
  --dart-define=TOPIC_PREFIX=yektahoosh/ds \
  ```
  
---

## نمونه اجرا با release
```bash

flutter build apk --release \
  --dart-define=BASE_URL=https://aparatchi.yektahoosh.com \
  --dart-define=CAPTURE_URL=https://aparatchi.yektahoosh.com/api/v1/tvscreen/capture \
  --dart-define=MQTT_URL=mqtt://mqtt1.yektahoosh.com:6000 \
  --dart-define=MQTT_USER=device_user \
  --dart-define=MQTT_PASS=SECRET \
  --dart-define=TOPIC_PREFIX=yektahoosh/ds \


```

</div>