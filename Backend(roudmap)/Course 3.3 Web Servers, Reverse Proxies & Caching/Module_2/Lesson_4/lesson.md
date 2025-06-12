## ⚡ الوحدة 2: التخزين المؤقت (Caching) وتحسين الأداء

### 📘 الدرس 4: تطبيق التخزين المؤقت باستخدام Redis

#### 🧠 **ماذا ستتعلم**

  * ما هو Redis ولماذا هو مناسب للتخزين المؤقت.
  * دورة حياة طلب يستخدم الكاش (Cache-Aside Pattern).
  * كيفية استخدام Redis في تطبيق Node.js لتخزين نتائج قاعدة البيانات مؤقتًا.
  * كيفية إبطال (invalidate) الكاش عند تحديث البيانات.

-----

### 🤔 1. ما هو Redis؟

Redis هو مخزن بيانات **في الذاكرة (in-memory)** سريع للغاية. نظرًا لأنه يخزن البيانات في ذاكرة الوصول العشوائي (RAM) بدلاً من القرص الصلب، فإن عمليات القراءة والكتابة تكون شبه فورية.

بينما يمكن استخدامه كقاعدة بيانات، فإن استخدامه الأكثر شيوعًا في تطبيقات الويب هو كـ **كاش موزع (distributed cache)** عالي الأداء.

**في بيئة التعلم الخاصة بنا:** يمكنك افتراض أن خادم Redis يعمل ومتاح لتطبيقك، وأن مكتبة `redis` لـ Node.js متاحة للاستخدام.

-----

### ⚙️ 2. دورة عمل الكاش (The Cache-Aside Pattern)

هذا هو النمط الأكثر شيوعًا لاستخدام الكاش مع قاعدة بيانات. عند وصول طلب لبيانات معينة (مثل `GET /users/123`):

1.  **ابحث في الكاش أولاً:** يحاول التطبيق جلب البيانات من Redis باستخدام مفتاح فريد (مثل `user:123`).
2.  **إصابة الكاش (Cache Hit):** إذا كانت البيانات موجودة في Redis، يتم إرجاعها مباشرة إلى العميل. **انتهت العملية.** (الطريق السريع ⚡)
3.  **إخفاق الكاش (Cache Miss):** إذا لم تكن البيانات موجودة في Redis...
    أ. يقوم التطبيق بإجراء الاستعلام المكلف من قاعدة البيانات الرئيسية (PostgreSQL).
    ب. **يخزن النتيجة في Redis** مع مدة صلاحية (TTL - Time To Live) حتى يتم استخدامها في الطلبات المستقبلية.
    ج. يتم إرجاع البيانات (التي تم جلبها من قاعدة البيانات) إلى العميل. (الطريق البطيء 🐢)

-----

### ✍️ 3. مثال عملي: التخزين المؤقت لطلبات API

لنفترض أن لدينا نقطة نهاية `GET /books/:id` تجلب كتابًا من قاعدة البيانات. سنضيف إليها منطق التخزين المؤقت باستخدام Redis.

```javascript
const express = require('express');
const redis = require('redis');
const db = require('./database'); // قاعدة بياناتنا الرئيسية

const app = express();

// افترض أن Redis يعمل على الإعدادات الافتراضية
const redisClient = redis.createClient();
redisClient.connect(); // قم بالاتصال بـ Redis عند بدء التطبيق

app.get('/books/:id', async (req, res) => {
  const { id } = req.params;
  const cacheKey = `book:${id}`; // مفتاح فريد للكاش

  try {
    // 1. ابحث في الكاش أولاً
    const cachedBook = await redisClient.get(cacheKey);

    if (cachedBook) {
      // 2. إصابة الكاش (Cache Hit)
      console.log('Serving from cache!');
      return res.json(JSON.parse(cachedBook));
    }

    // 3. إخفاق الكاش (Cache Miss) - اذهب إلى قاعدة البيانات
    console.log('Serving from database...');
    const { rows } = await db.query('SELECT * FROM books WHERE id = $1', [id]);
    const book = rows[0];

    if (!book) {
      return res.status(404).send('Book not found');
    }

    // 4. خزّن النتيجة في Redis مع صلاحية لمدة ساعة (3600 ثانية)
    await redisClient.set(cacheKey, JSON.stringify(book), {
      EX: 3600, // EX for seconds
    });
    
    res.json(book);

  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

app.listen(3000);
```

-----

### 🗑️ 4. إبطال الكاش (Cache Invalidation)

هذا هو الجزء الحاسم\! إذا قام مستخدم بتحديث كتاب (`PUT /books/:id`)، فإن البيانات الموجودة في الكاش لهذا الكتاب تصبح قديمة (stale). يجب علينا حذفها.

**في معالج طلب `PUT`:**

```javascript
app.put('/books/:id', async (req, res) => {
    const { id } = req.params;
    const { title, author } = req.body;
    const cacheKey = `book:${id}`;

    // 1. قم بتحديث قاعدة البيانات الرئيسية أولاً
    const { rows } = await db.query(
        'UPDATE books SET title = $1, author = $2 WHERE id = $3 RETURNING *',
        [title, author, id]
    );

    // 2. إذا نجح التحديث، قم بإبطال (حذف) الكاش
    await redisClient.del(cacheKey);
    console.log('Cache invalidated for book:', id);

    res.json(rows[0]);
});
```

الآن، أي طلب `GET` تالٍ لنفس الكتاب سيجد الكاش فارغًا (Cache Miss)، وسيجلب البيانات المحدثة من قاعدة البيانات، ثم يعيد تخزينها في الكاش.

-----