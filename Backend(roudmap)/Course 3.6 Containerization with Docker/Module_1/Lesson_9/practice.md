### 🛠️ تمرين عملي
1.  تأكد من أن لديك حساب في Docker Hub.
2.  خذ إحدى الصور التي بنيتها في الدروس السابقة (مثل `my-dev-app`).
3.  في طرفيتك، سجل دخولك باستخدام `docker login`.
4.  أعد وسم صورتك باستخدام اسم المستخدم الخاص بك: `docker tag my-dev-app:latest your-username/my-first-app:1.0`.
5.  ادفع الصورة الموسومة إلى Docker Hub: `docker push your-username/my-first-app:1.0`.
6.  (للتحقق) اذهب إلى ملفك الشخصي على موقع Docker Hub ويجب أن ترى المستودع الجديد.
7.  (للتحقق) قم أولاً بحذف الصورة من جهازك المحلي (`docker rmi your-username/my-first-app:1.0`)، ثم حاول تشغيلها مرة أخرى باستخدام `docker run`. ستلاحظ أن Docker يقوم الآن بسحبها من الإنترنت.

---
