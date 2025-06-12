## 🗃️ الوحدة 3: ربط قواعد البيانات مع Node.js

### 📘 الدرس 1: الاتصال بـ PostgreSQL من Node.js

#### 🧠 **ماذا ستتعلم**
* ما هو دور مشغل قاعدة البيانات (Database Driver).
* كيفية تثبيت وإعداد مكتبة `node-postgres` (الحزمة `pg`).
* كيفية الاتصال بقاعدة البيانات باستخدام مجمع الاتصالات (Connection Pool).
* كيفية تنفيذ استعلام `SELECT` ومعالجة النتائج.
* كيفية تنفيذ استعلامات مُمَعلمَة (Parameterized Queries) لمنع حقن SQL.

---
### 🌉 1. الجسر: مشغل قاعدة البيانات (Database Driver)
لكي يتمكن تطبيق Node.js من التحدث مع قاعدة بيانات PostgreSQL، فإنه يحتاج إلى "مترجم" أو "وسيط". هذا الوسيط يسمى **مشغل قاعدة البيانات (Database Driver)**. إنه ببساطة مكتبة برمجية (حزمة npm في حالتنا) تسمح لتطبيقك بإرسال أوامر SQL إلى قاعدة البيانات واستقبال النتائج.

أشهر وأقوى مشغل لـ PostgreSQL في بيئة Node.js هو **`node-postgres`**، والذي يتم تثبيته من npm باسم الحزمة `pg`.

---
### ⚙️ 2. الإعداد والاتصال

#### **الخطوة 1: تثبيت الحزمة**
في مشروع Node.js/Express الخاص بك، قم بتثبيت الحزمة:
```bash
npm install pg
```

#### **الخطوة 2: إنشاء مجمع الاتصالات (Connection Pool)**
بدلاً من إنشاء اتصال جديد مع قاعدة البيانات لكل استعلام (وهي عملية بطيئة ومكلفة)، من الأفضل استخدام **مجمع اتصالات (Connection Pool)**. يقوم المجمع بإنشاء عدد من الاتصالات الجاهزة وإبقائها مفتوحة. عندما يحتاج تطبيقك إلى تنفيذ استعلام، فإنه "يستعير" اتصالاً من المجمع ويعيده عند الانتهاء. هذا يجعل العملية أسرع وأكثر كفاءة.

من الأفضل وضع إعدادات الاتصال في ملف منفصل (مثل `db.js`):
```javascript
// db.js
const { Pool } = require('pg');

const pool = new Pool({
  user: 'postgres', // اسم المستخدم لقاعدة بياناتك
  host: 'localhost',
  database: 'my_first_db', // اسم قاعدة البيانات التي أنشأناها
  password: 'your_password', // كلمة المرور التي عينتها أثناء التثبيت
  port: 5432,
});

module.exports = pool;
```
> **ملاحظة أمان:** في التطبيقات الحقيقية، لا تضع بيانات الاعتماد مباشرة في الكود. استخدم متغيرات البيئة (Environment Variables) بدلاً من ذلك.

---
### ⚡ 3. تنفيذ الاستعلامات
الآن بعد أن أصبح لدينا `pool`، يمكننا استخدامه لتنفيذ الاستعلامات باستخدام دالة `pool.query()`. هذه الدالة غير متزامنة وتُرجع Promise.

**مثال: جلب البيانات في تطبيق Express**
```javascript
// server.js
const express = require('express');
const pool = require('./db'); // استيراد المجمع الذي أنشأناه
const app = express();

app.get('/users', async (req, res) => {
  try {
    const result = await pool.query('SELECT * FROM users');
    // البيانات الفعلية تكون في الخاصية .rows
    res.status(200).json(result.rows);
  } catch (err) {
    console.error(err.message);
    res.status(500).send('Server Error');
  }
});

// ... app.listen ...
```
---
### 🛡️ 4. الاستعلامات المُمَعلمَة وأمان SQL
**حقن SQL (SQL Injection)** هو هجوم أمني خطير يحدث عندما يتمكن المستخدم من إدخال كود SQL خبيث في استعلامك.

**مثال على كود غير آمن:**
```javascript
// لا تفعل هذا أبدًا!
const userInput = "1; DROP TABLE users; --";
const query = `SELECT * FROM users WHERE id = ${userInput}`;
// سينفذ هذا الأمر حذف جدول المستخدمين!
```
**الحل هو الاستعلامات المُمَعلمَة (Parameterized Queries):**
لا تقم أبدًا بدمج مدخلات المستخدم مباشرة في سلسلة نصية للاستعلام. بدلاً من ذلك، استخدم علامات placeholders (`$1`, `$2`, etc.) ومرر القيم في مصفوفة منفصلة. يقوم المشغل (`pg`) بمعالجة هذه القيم بشكل آمن، مما يمنع أي هجوم.

**مثال آمن:**
```javascript
app.get('/users/:id', async (req, res) => {
  const { id } = req.params;
  try {
    const queryText = 'SELECT * FROM users WHERE id = $1';
    const result = await pool.query(queryText, [id]); // تمرير القيمة في مصفوفة
    
    if (result.rows.length === 0) {
      return res.status(404).send('User not found');
    }
    res.json(result.rows[0]);
  } catch (err) {
    console.error(err.message);
    res.status(500).send('Server Error');
  }
});
```
---
