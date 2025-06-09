## ✅ الدرس 3: Promises و Async/Await - تمارين عملية

### 🧪 تمارين تدريبية

* ✍️ اكتب سلسلة من دوال الـ `Callbacks` تقوم بـ:
    1.  قراءة اسم المستخدم.
    2.  التحقق من كلمة المرور.
    3.  عرض رسالة ترحيب.
    * 💡 *التلميح: أنشئ كل دالة لتأخذ معاملًا ودالة رد نداء (callback).*

* ✍️ عدّل التمرين السابق لاستخدام `Promises` بدلًا من `Callbacks`.
    * 💡 *التلميح: غيّر كل دالة لتُرجع `Promise` واستخدم `.then()` لربط السلسلة.*

* ✍️ حوّل الكود التالي إلى استخدام `Async/Await`:
    `fetchData().then(data => process(data)).then(result => display(result)).catch(err => console.error(err));`
    * 💡 *التلميح: استخدم `await` بدلًا من `.then()`، و `try/catch` لمعالجة الأخطاء.*

* ✍️ أنشئ دالة تستخدم `setTimeout` داخل `Promise` لإرجاع رسالة "Done" بعد ثانيتين.
    * 💡 *التلميح: لفّ `setTimeout` داخل `new Promise(resolve => ...)`.*

***

