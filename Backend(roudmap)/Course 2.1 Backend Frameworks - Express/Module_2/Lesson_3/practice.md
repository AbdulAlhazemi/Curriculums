### 🛠️ تمرين عملي
1.  أنشئ خادم Express وتأكد من استخدام الـ Middleware `app.use(express.json());` في الأعلى.
2.  أنشئ مسارًا `POST /echo`.
3.  داخل دالة المعالج، قم باستخلاص المعلومات التالية من كائن `req`:
    * جسم الطلب (`req.body`).
    * قيمة ترويسة `Content-Type` (`req.headers['content-type']`).
    * قيمة سلسلة استعلام اختيارية اسمها `source` (`req.query.source`).
4.  أرسل استجابة **JSON** برمز حالة `200` تحتوي على جميع المعلومات التي استخلصتها. يجب أن تبدو الاستجابة كالتالي:
    ```json
    {
      "receivedData": { "... a JSON object ..." },
      "requestContentType": "application/json",
      "sourceFrom": "postman"
    }
    ```
5.  استخدم عميل API (مثل Postman أو Thunder Client) لاختبار نقطة النهاية `POST /echo?source=postman` عن طريق إرسال جسم JSON مع الطلب.

> **تلميح:** تذكر أن `res.status()` تُعيد كائن `res`، مما يسمح لك بربطها مع `res.json()` في سطر واحد: `res.status(200).json(...)`.

---