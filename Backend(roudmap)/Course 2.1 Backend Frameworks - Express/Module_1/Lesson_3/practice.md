### 🛠️ تمرين عملي
1.  قم بإعداد خادم Express جديد (كما في الدرس السابق).
2.  أنشئ واجهة API بسيطة لكتب (`/books`).
3.  أضف مسار `GET /books` ليرسل استجابة "Fetching all books".
4.  أضف مسار `POST /books` ليرسل استجابة "New book added".
5.  أضف مسار `DELETE /books/1` ليرسل استجابة "Book with ID 1 deleted".
6.  استخدم أداة مثل Postman أو Thunder Client لاختبار كل مسار من هذه المسارات والتأكد من أنك تحصل على الاستجابة الصحيحة.

> **تلميح:** تذكر أن لكل فعل HTTP دالة خاصة به في Express (`app.get`, `app.post`, `app.delete`, etc.).

---
