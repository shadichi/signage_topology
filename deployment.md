# Deployment — Digital Signage

## هدف
این بخش نحوه‌ی استقرار (Deployment) سیستم Digital Signage را توضیح می‌دهد  

---

## محیط‌ها (Environments)
1. **Development (Dev)**  
   - در عمل اپ رو روی سیستم خودمان یا مستقیم روی تلویزیون Build و Run می‌کنیم.
(هیچ سرور جدا یا محیط مجزا وجود ندارد.) 

2. **Staging (Pre-Production)**  
   - فعلاً محیط جدا نداریم، تست‌ ها را روی همان سرور اصلی انجام می‌ دهیم.

3. **Production (Prod)**  
   - همان نسخه‌ای که روی تلویزیون‌ ها نصب میشه.
اپ Flutter با دستور flutter build apk --release ساخته و مستقیم روی دستگاه نصب میشه.  
