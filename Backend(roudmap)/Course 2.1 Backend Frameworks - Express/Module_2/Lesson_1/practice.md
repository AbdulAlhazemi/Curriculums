### 🛠️ تمرين عملي
1.  أنشئ مشروع Express جديدًا وقم بتثبيت `morgan`.
2.  استخدم `app.use(morgan('tiny'));` في ملف `index.js` لتسجيل جميع الطلبات بتنسيق بسيط.
3.  اكتب دالة Middleware مخصصة تقوم بإضافة خاصية جديدة إلى كائن الطلب، مثل `req.requestTime = new Date().toLocaleTimeString()`. لا تنسَ استدعاء `next()`.
4.  استخدم الـ Middleware المخصص الذي أنشأته عبر `app.use()`.
5.  في مسار `GET /`، أرسل استجابة تحتوي على وقت الطلب الذي أضفته: `res.send(`This request was received at: ${req.requestTime}`);`.
6.  شغل الخادم واختبره. تحقق من طرفيتك لترى سجلات `morgan`، وتحقق من المتصفح لترى رسالة الوقت.

---