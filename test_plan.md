# Tests Plan — Digital Signage (TV App)

## وضعیت فعلی
- در حال حاضر **هیچ تست خودکاری پیاده‌سازی نشده**.

---

## انواع تست‌ها

### 1) Unit Tests 
- UseCaseها و Repositoryها:
  - `LoadScheduleUseCase` → اگر API خالی داد، state باید “NoSchedule” شود.
  - `AssetsRepo.verifyChecksum` → ورودی خراب → false.
  - Backoff/Retry روی خطای 5xx → تعداد تلاش‌ها محدود.
- Helpers:
  - پارسنگ زمان UTC، محاسبه t0.

### 2) Widget Tests 
- Home Screen: نمایش وضعیت دانلود.
- Video Screen: نمایش دکمه‌ها/اسپینر آماده‌ سازی.

### 3) Integration Tests 
- Happy path: دریافت برنامه → کش → شروع پخش.
- MQTT action: دریافت “pause” → توقف پخش؛ “play” → ادامه.
- Capture: دستور capture → ارسال موفق multipart و status 200.

### 4) Manual Checklist 
- اپ نصب و اجرا می‌شود.
- اتصال MQTT برقرار می‌شود (log).
- برنامه فعال دریافت می‌شود (۳ آیتم نمونه).
- یک ویدیو دانلود و اجرا می‌شود.
- دستور capture از پنل → سرور 200 می‌دهد.

---


## ابزار و کتابخانه‌ها
- `flutter_test` (پیش‌فرض)
- `mocktail` یا `mockito` برای موک HTTP/MQTT
- (اختیاری) `fake_async` برای شبیه‌سازی زمان
- (اختیاری) `golden_toolkit` برای گلدن تست‌ها

---

## اجرا
- همه تست‌ها:
flutter test
- فقط یک فایل:
flutter test test/usecases/load_schedule_test.dart

---

## اسکلت نمونه (Unit) — UseCase زمان
```dart
import 'package:flutter_test/flutter_test.dart';

void main() {
  test('compute t0 from server time', () {
    // arrange
    final serverUtc = DateTime.parse('2025-08-31T06:00:00Z');
    // act
    final t0 = serverUtc; // این‌جا تابع واقعی‌ت رو صدا بزن
    // assert
    expect(t0.isUtc, true);
  });
}
