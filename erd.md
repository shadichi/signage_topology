# Database ER Diagram — Digital Signage (Local)

## هدف
فعلاً ذخیره‌سازی محلی به‌صورت Key–Value (SharedPreferences/XML) است. این سند:
1) مدل منطقی داده‌ها (ERD مفهومی) را نشان می‌دهد؛  
2) نگاشت آن به کلیدهای واقعی در SharedPreferences را لیست می‌کند.

---


## توضیح درباره ERD

در حال حاضر دیتابیس ما **ساختار رابطه‌ای (Relational)** مثل MySQL یا PostgreSQL ندارد،  
بلکه فقط از **SharedPreferences (Key–Value Store)** استفاده می‌کنیم.  

به همین دلیل:

- **مدل موجودیت–رابطه (ERD)** که معمولاً برای جداول و کلیدهای خارجی کشیده می‌شود، در اینجا کاربرد ندارد.  
- داده‌ها در قالب **کلید–مقدار** ساده نگه‌داری می‌شوند (مثلاً `flutter.id`, `state`, `video_0_0` …).  
- بنابراین ERD رسمی نمی‌شود کشید، مگر اینکه اول داده‌ها را به یک دیتابیس جدولی (Hive/Isar/SQLite) منتقل کنیم.

---

## نتیجه
به‌جای ERD کامل، همین **لیست کلیدها و JSON نمونه** مستند شده است.  

---

## نوع ذخیره‌سازی فعلی
- SharedPreferences (XML)
- نمونه فعلی:
  ```xml
  <?xml version='1.0' encoding='utf-8' standalone='yes' ?>
  <map>
      <string name="flutter.id">ixgwe.ioyvw.ss4mr</string>
  </map>

  
