## 🟩 الوحدة 3: أساسيات Node.js

### 📘 الدرس 3: وحدات Node.js الأساسية (Core Modules)

#### 🧠 **ماذا ستتعلم؟**
* ما هي وحدات Node.js الأساسية.
* كيفية استيرادها واستخدامها باستخدام `require`.
* التعرف على وحدات مهمة مثل:
    * `fs` (نظام الملفات)
    * `path` (مسارات الملفات)
    * `http` (إنشاء خوادم)
    * `os` (معلومات النظام)
    * `events` (نظام الأحداث)
* بناء تطبيق بسيط باستخدام وحدات أساسية.

***

### 1. ما هي وحدات Node.js الأساسية؟

**Core Modules** هي وحدات مدمجة داخل Node.js، يمكنك استخدامها مباشرة دون تثبيت أي مكتبة.

✅ لا تحتاج إلى تثبيت عبر `npm install`
❗ فقط استوردها باستخدام `require`

***

### 2. استخدام `require` لاستيراد الوحدات

```javascript
const fs = require('fs');
const path = require('path');
```
تستخدم `require()` لتحميل الوحدة وتخزينها في متغير.

***

### 3. وحدة `fs` – نظام الملفات

تمكنك من قراءة وكتابة الملفات.

```javascript
const fs = require('fs');

// Create a dummy file for the example
fs.writeFileSync('example.txt', 'Hello from fs module!');

fs.readFile('example.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```
> 📌 تستخدم `fs.writeFile`, `fs.readFile`, `fs.unlink` وغيرها.

***

### 4. وحدة `path` – التعامل مع المسارات

مفيدة لبناء مسارات آمنة ومتوافقة مع أنظمة التشغيل.

```javascript
const path = require('path');

const filePath = path.join(__dirname, 'folder', 'file.txt');
console.log(filePath);
```

***

### 5. وحدة `http` – إنشاء خادم بسيط

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  res.end("مرحبًا من خادم Node.js");
});

server.listen(3000, () => {
  console.log("الخادم يعمل على http://localhost:3000");
});
```
> 🟢 تستخدم لبناء API أو صفحات ويب بسيطة.

***

### 6. وحدة `os` – معلومات النظام

```javascript
const os = require('os');

console.log(os.platform()); // e.g., 'win32', 'linux'
console.log(os.freemem());  // Free memory in bytes
```
تُستخدم للحصول على معلومات حول نظام التشغيل.

***

### 7. وحدة `events` – نظام الأحداث

```javascript
const EventEmitter = require('events');

const emitter = new EventEmitter();

emitter.on('greet', () => {
  console.log("مرحبًا، تم إطلاق الحدث!");
});

emitter.emit('greet');
```
> 🌀 مفيدة لبناء نماذج قائمة على الأحداث (Event-driven architecture).

***