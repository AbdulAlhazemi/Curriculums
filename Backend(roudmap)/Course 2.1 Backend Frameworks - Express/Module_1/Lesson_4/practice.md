### 🛠️ تمرين عملي
1.  أنشئ خادم Express جديدًا.
2.  أنشئ مسارًا `GET /artists/:artistId` يأخذ معرف الفنان من `req.params` ويرسل استجابة مثل: `Fetching albums for artist: [artistId]`.
3.  أنشئ مسارًا `GET /songs` يتعامل مع سلاسل الاستعلام الاختيارية.
    * إذا كان عنوان URL هو `/songs?genre=rock`، يجب أن تكون الاستجابة `Fetching songs in genre: rock`.
    * إذا كان عنوان URL هو `/songs` فقط، يجب أن تكون الاستجابة `Fetching all songs`.
4.  اختبر كلا المسارين باستخدام متصفحك أو عميل API.

> **تلميح:** للمهمة الثانية، ستحتاج إلى استخدام جملة `if` للتحقق مما إذا كان `req.query.genre` موجودًا أم لا.

---
