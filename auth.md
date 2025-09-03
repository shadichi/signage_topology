# Authentication / Authorization — Digital Signage

## هدف
این داکیومنت توضیح می‌دهد چه کسی چطور احراز هویت می‌شود (AuthN) و چه چیزی اجازه دارد انجام دهد (AuthZ). تمرکز ما روی دو هویت است: **ادمین پنل** و **دستگاه TV**.

---

## هویت‌ها (Identities)
- **Admin (Panel User):** ورود به پنل مدیریت، تعریف TV و اختصاص Action Group.
- **Device (TV App):** اپ Flutter نصب‌شده روی تلویزیون. یک «کد/سریال دستگاه» دارد و روی MQTT مشترک می‌شود.

---

## سناریو A — ثبت و آماده‌سازی دستگاه (Provisioning)
1) **نمایش سریال در TV:**  
   اپ پس از نصب، یک `TV_CODE` نمایش می‌دهد.

2) **ثبت در پنل توسط ادمین:**  
   ادمین وارد پنل شده، TV جدید را با `TV_CODE` اضافه می‌کند و برای آن یک **Action Group** تعریف/اختصاص می‌دهد.

3) **تنظیمات MQTT:**  
   - اپ با `MQTT_USER` و `MQTT_PASS` به Broker وصل می‌شود (Basic Auth).  
   - اپ روی تاپیک‌های مخصوص همان دستگاه مشترک می‌شود:  
     - `yektahoosh/ds/<TV_CODE>/actiongroup`  
     - `yektahoosh/ds/<TV_CODE>/splash`  
     - `yektahoosh/ds/<TV_CODE>/sync`  
     - `yektahoosh/ds/<TV_CODE>/changelockstate`  
     - `yektahoosh/ds/<TV_CODE>/capture`  
     - (سراسری) `yektahoosh/ds/getlockstate`

4) **اعتبارسنجی سمت سرور:**  
   سرور/بک‌اند فقط به دستگاه‌هایی اجازه مصرف می‌دهد که `TV_CODE` آنها در پنل ثبت شده باشد.

---


## سناریو C — ورود ادمین به پنل
- **Panel Login:**  
  - SSO  
  - مجوزها: فقط نقش‌های ادمین می‌توانند TV جدید ثبت کنند و Action Group بدهند.

---

## سناریو D — قفل و دسترسی (Lock State)
- تاپیک‌های مرتبط:  
  - `yektahoosh/ds/<DEVICE_CODE>/changelockstate`  
  - `yektahoosh/ds/getlockstate`
- مجوز: فقط پیام‌های صادرشده از پنل معتبرند. دستگاه صرفاً وضعیت قفل را اعمال/گزارش می‌کند.

---

## دنباله‌ی نمونه‌ها (Sequence)

### 1) Provisioning (ثبت دستگاه)
```mermaid
sequenceDiagram
  participant TV as TV App
  participant Panel as Admin Panel
  participant MQTT as MQTT Broker
  participant API as Backend API

  TV->>TV: show DEVICE_CODE
  Panel->>API: POST /v1/devices (DEVICE_CODE)
  API-->>Panel: 201 created

  TV->>MQTT: CONNECT (Basic Auth)
  MQTT-->>TV: CONNACK success

  Panel->>API: assign ActionGroup to DEVICE_CODE
  API-->>MQTT: publish actiongroup message to topic of DEVICE_CODE
  MQTT-->>TV: actiongroup message
```