# Build Manual — Digital Signage (Flutter TV)

## هدف
راهنمای سریع برای ساخت (Build) اپ Android TV و نصب روی دستگاه ‌ها.

---

## پیش‌نیازها
- Flutter SDK نصب و روی PATH
- Android Studio + Android SDK Platform-Tools
- JDK (ترجیحاً Temurin 17)
- یک دستگاه Android TV یا امولاتور TV
- فعال بودن USB debugging / ADB روی TV

---

## build برای دیباگ (اجرای سریع)
flutter run

## build ریلیز (APK)
flutter build apk --release

## versioning
- `version: x.y.z+code` در `pubspec.yaml`

مثال:
version: 1.2.0+34


