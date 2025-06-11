## 🟩 الوحدة 3: أساسيات Node.js

### 📘 الدرس 6: وحدات Node.js الأساسية (Core Modules) - مراجعة

#### 🧠 ماذا ستتعلم؟
* ما هي الوحدات الأساسية في Node.js.
* التعرف على وحدات مثل `fs`، `path`، `http`، `events`، و`stream`.
* كيفية استخدام هذه الوحدات في مشاريعك.
* فهم أهمية كل وحدة ووظيفتها.

---
### 1. ما هي الوحدات الأساسية في Node.js؟
Node.js يأتي مع مجموعة كبيرة من الوحدات المدمجة (**Core Modules**) التي يمكنك استخدامها بدون تثبيت أي شيء إضافي. هذه الوحدات توفر وظائف مهمة لبناء تطبيقات الخوادم، والتعامل مع الملفات والشبكات، وغيرها.

---
### 2. أشهر الوحدات الأساسية
* **fs**: للتعامل مع نظام الملفات (قراءة، كتابة، حذف، تعديل الملفات).
* **path**: لتسهيل التعامل مع مسارات الملفات والمجلدات.
* **http**: لإنشاء خوادم ويب وتلقي طلبات HTTP.
* **events**: لإنشاء وإدارة الأحداث (Event-driven programming).
* **stream**: للتعامل مع تدفقات البيانات (مثل قراءة ملف كبير جزءًا بجزء).

---
### 3. كيف تستخدم الوحدة الأساسية؟
تستخدم دالة `require` لتحميل الوحدة:
```javascript
const fs = require('fs');
```
**مثال: قراءة محتوى ملف نصي:**
```javascript
const fs = require('fs');

// Note: Create an 'example.txt' file for this to work.
fs.readFile('example.txt', 'utf8', (err, data) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log(data);
});
```

---
### 4. مثال باستخدام وحدة `http` لإنشاء خادم ويب بسيط
```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain; charset=utf-8');
  res.end('مرحباً من خادم Node.js!');
});

server.listen(3000, () => {
  console.log('Server running at http://localhost:3000/');
});
```

---
