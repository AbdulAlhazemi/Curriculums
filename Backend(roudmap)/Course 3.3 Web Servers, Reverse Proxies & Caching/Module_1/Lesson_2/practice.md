### 🛠️ تمرين عملي
1.  افتح الطرفية في بيئة التعلم الخاصة بك.
2.  تحقق من حالة خدمة Nginx باستخدام الأمر `sudo systemctl status nginx`. لاحظ أنها يجب أن تكون `active (running)`.
3.  أوقف الخدمة باستخدام الأمر `sudo systemctl stop nginx`.
4.  الآن، حاول زيارة `http://localhost` في متصفحك. ماذا يحدث؟ (يجب أن يفشل الاتصال).
5.  أعد تشغيل الخدمة باستخدام `sudo systemctl start nginx`.
6.  قم بتحديث الصفحة في متصفحك للتأكد من أن صفحة الترحيب قد عادت للظهور.

---
