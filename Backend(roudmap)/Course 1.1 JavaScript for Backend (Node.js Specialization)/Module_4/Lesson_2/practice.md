### 🛠️ تمرين عملي (Practice)
1.  أنشئ ملفًا يحتوي على دالة تقوم بقراءة ملف غير موجود باستخدام `fs.promises.readFile`.
2.  أضف `debugger;` داخل كتلة `catch`.
3.  شغّل البرنامج باستخدام `node inspect app.js`.
4.  حاول تتبع الخطأ باستخدام `repl` لفحص كائن الخطأ `err`.
5.  كرر العملية باستخدام Visual Studio Code مع وضع نقطة توقف داخل `catch`.

> 💡 **تلميح:** استخدم دالة غير متزامنة مع `try/catch` لتتمكن من استخدام `debugger` أو نقاط التوقف بشكل فعال عند حدوث الخطأ.

***