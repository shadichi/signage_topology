<div dir="rtl">

# MQTT and HTTPS Agreements — Digital Signage

## هدف
 قراردادهای ارتباطی اپ TV با سرور:
- ارتباط **HTTPS** برای درخواست‌ های HTTP (مثل آپلود اسکرین‌ شات).
- ارتباط **MQTT** برای پیام‌های لحظه‌ ای (sync، lock state، splash و …).

---

## 1. HTTPS — قراردادها

### Base URL
https://aparatchi.yektahoosh.com/api/v1

### Endpoints 
- **POST /tvscreen/capture**  
  - هدف: ارسال اسکرین‌شات  
  - بادی: `multipart/form-data` شامل:  
    - `screenshot` (png)  
    - `requestID`  


- **GET /time**  
  - هدف: همگام‌سازی زمان دستگاه‌ها  
  - پاسخ: UTC timestamp 
---

## 2. MQTT — قراردادها

mqtt://mqtt1.yektahoosh.com:6000

### Auth
- اتصال با **Basic Auth** (username/password)
- فقط دستگاه‌هایی که در پنل ثبت شده‌اند معتبرند

### تاپیک‌ها
| Topic                                | توضیح                          | Payload |
|--------------------------------------|-------------------------------|---------|
| yektahoosh/ds/<TV_CODE>/actiongroup | اختصاص Action Group            | JSON |
| yektahoosh/ds/<TV_CODE>/splash      | نمایش Splash Screen            | - |
| yektahoosh/ds/<TV_CODE>/sync        | دستور Sync با سرور             | - |
| yektahoosh/ds/<TV_CODE>/changelockstate | تغییر وضعیت قفل               | String LOCK/UNLOCK |
| yektahoosh/ds/getlockstate              | درخواست وضعیت قفل             | - |
| yektahoosh/ds/<TV_CODE>/capture     | دستور گرفتن اسکرین‌ شات        | - |

</div>