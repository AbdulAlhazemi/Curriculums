### 🛠️ تمرين عملي
1.  في نفس المشروع السابق، أنشئ مجلدًا جديدًا داخل `public` باسم `images`.
2.  ضع أي صورة صغيرة داخل مجلد `public/images` (مثلاً `logo.png`).
3.  عدّل ملف `public/index.html` وأضف وسم `<img>` لعرض هذه الصورة.
    ```html
    <img src="/images/logo.png" alt="My Logo">
    ```
4.  أعد تشغيل الخادم وقم بتحديث الصفحة في متصفحك. يجب أن ترى الصورة معروضة الآن.

> **تلميح:** لاحظ أنك في ملف HTML، لا تحتاج إلى كتابة `/public` في مسارات الملفات (مثل `href` و `src`). Express يتعامل مع مجلد `public` كنقطة بداية (root) للملفات الثابتة.

---