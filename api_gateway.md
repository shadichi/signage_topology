# API Gateway or Routing Design — Digital Signage

## هدف
این قسمت نحوه ارتباط اپ TV با سرور را توضیح می‌دهد: آدرس ها، هدرها، ثبت دستگاه، MQTT Topic and Message، Routing Design. 

---

## URLs

  - mqtt://mqtt1.yektahoosh.com:6000 (for MQTT req)
  - https://aparatchi.yektahoosh.com/api/v1/tvscreen/capture (for sending screenshot of video)

---

## هدرهای استاندارد
- Authorization: Basic Auth (just for MQTT)
- Content-Type: multipart/form-data
- Accept: application/json

---

## ثبت دستگاه

   - ابتدا سریال یکتای تولید شده توسط اپلیکیشن نمایش داده میشود و ادمین موظف است آن را در قسمت افزودن تلویزیون پنل ادمین ثبت کند
   - سپس باید به تلویزیون مذکور یک اکشن گروپ اختصاص دهد تا دیتا توسط MQTT به تلویزیون سابسکرایب کرده ارسال شود.
   - اپ سریال را در Secure Storage نگه می دارد
   - همه درخواست ها با هدر Basic Auth

---

## MQTT Topic and Message

| Path                         | توضیح کوتاه                         | Message |
-------------------------------|-------------------------------------|-----|
 yektahoosh/ds/TV-Code/actiongroup      | گرفتن اکشن گروپ  | TV-Code |
 yektahoosh/ds/TV-Code/splash           | نمایش اسپلش اسکرین    | - |
 yektahoosh/ds/TV-Code/sync           | سینک شدن TV با سرور | - |
 yektahoosh/ds/TV-Code/changelockstate  | تغییر وضعیت قفل بودن دستگاه  | - |
 yektahoosh/ds/getlockstate            | برگرداندن وضعیت قفل اپلیکیشن| - |
 yektahoosh/ds/TV-Code/capture            | گرفتن اسکرین شات و ارسال به سرور  | - |

در پاسخ های مربوط به ویدیو  لینک دانلود از CDN برگردانده می شود. اپ مستقیم از CDN دانلود می کند.

---

## Routing Design
```mermaid
sequenceDiagram
  participant TV as TV App
  participant API as Backend API
  participant MQTT as MQTT Broker
  participant CDN as CDN

  TV->>API: POST /api/v1/tvscreen/capture (multipart/form-data)
  API-->>TV: 200 Upload OK / JSON Response

  TV->>MQTT: SUBSCRIBE yektahoosh/ds/TV-Code/actiongroup (Basic Auth)
  MQTT-->>TV: ActionGroup message

  TV->>MQTT: SUBSCRIBE yektahoosh/ds/TV-Code/splash
  MQTT-->>TV: Show Splash command

  TV->>MQTT: SUBSCRIBE yektahoosh/ds/TV-Code/sync
  MQTT-->>TV: Sync request

  TV->>MQTT: SUBSCRIBE yektahoosh/ds/TV-Code/changelockstate
  MQTT-->>TV: LockState change

  TV->>MQTT: SUBSCRIBE yektahoosh/ds/getlockstate
  MQTT-->>TV: Current lock state

  TV->>MQTT: SUBSCRIBE yektahoosh/ds/TV-Code/capture
  MQTT-->>TV: Trigger screenshot capture

  TV->>CDN: GET video files by URL
  CDN-->>TV: 200 video content


