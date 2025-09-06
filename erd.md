# Database ER Diagram — Digital Signage (Local)

## هدف
فعلاً ذخیره‌ سازی محلی به‌ صورت Key–Value (SharedPreferences/XML) است.

---


## توضیح درباره ERD

در حال حاضر دیتابیس ما ساختار رابطه‌ای ندارد 
بلکه فقط از **SharedPreferences (Key–Value Store)** استفاده می‌کنیم.

به همین دلیل:

-  ERD  معمولاً برای جداول و کلیدهای خارجی کشیده می‌شود، در اینجا کاربرد ندارد.  
- داده‌ها در قالب **کلید–مقدار** ساده نگه‌داری می‌ شوند (مثلاً `flutter.id`, `state`, `video_0_0` …).  
- بنابراین ERD رسمی نمی‌شود کشید، مگر اینکه اول داده‌ ها را به یک دیتابیس جدولی (Hive/Isar/SQLite) منتقل کنیم.

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

  
