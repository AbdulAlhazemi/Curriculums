## 🚀 الوحدة 1: أساسيات Express.js

### 📘 الدرس 2: إعداد مشروع Express.js

#### 🧠 **ماذا ستتعلم**
* كيفية تهيئة مشروع Node.js جديد باستخدام `npm init`.
* كيفية تثبيت حزمة Express باستخدام `npm install express`.
* دور ملف `package.json` ومجلد `node_modules`.
* كيفية كتابة وتشغيل خادم "Hello World" بسيط باستخدام Express.

---
### 📋 1. المتطلبات الأساسية
قبل أن نبدأ، تأكد من أن لديك الأدوات التالية مثبتة على جهازك:
* **Node.js و npm:** يمكنك تحميلهما من [الموقع الرسمي لـ Node.js](https://nodejs.org/).
* **محرر أكواد:** مثل VS Code.
* **طرفية (Terminal):** مثل Git Bash على ويندوز، أو الطرفية الافتراضية على macOS و Linux.

---
### ⚙️ 2. خطوات إعداد المشروع

#### **الخطوة 1: إنشاء مجلد المشروع**
افتح الطرفية الخاصة بك ونفذ الأمرين التاليين لإنشاء مجلد جديد والدخول إليه.
```bash
mkdir my-express-app
cd my-express-app
```

#### **الخطوة 2: تهيئة مشروع Node.js**
الآن، سنقوم بتهيئة المشروع. هذا ينشئ ملف `package.json` الذي يحتوي على معلومات حول مشروعنا والتبعيات (packages) التي يستخدمها.
```bash
# الخيار -y يعني الموافقة على جميع الإعدادات الافتراضية
npm init -y
```
بعد تنفيذ هذا الأمر، سترى ملفًا جديدًا اسمه `package.json` داخل مجلدك.

#### **الخطوة 3: تثبيت Express**
الآن سنقوم بتثبيت حزمة Express من سجل npm.
```bash
npm install express
```
هذا الأمر يقوم بشيئين رئيسيين:
1.  ينشئ مجلدًا جديدًا اسمه `node_modules` حيث يتم تخزين كود Express وجميع الحزم التي يعتمد عليها.
2.  يضيف `express` تلقائيًا إلى قسم `dependencies` في ملف `package.json`.

#### **الخطوة 4: إنشاء ملف الخادم**
أنشئ ملفًا جديدًا ليكون نقطة انطلاق الخادم الخاص بك. سنسميه `index.js`.
```bash
touch index.js
```

---
### ✍️ 3. كتابة خادم "Hello World"
افتح ملف `index.js` في محرر الأكواد الخاص بك والصق الكود التالي:

```javascript
// 1. استيراد حزمة Express
const express = require('express');

// 2. إنشاء نسخة من تطبيق Express
const app = express();

// 3. تحديد رقم المنفذ (Port) الذي سيعمل عليه الخادم
const port = 3000;

// 4. تعريف مسار (Route) للتعامل مع طلبات GET على المسار الجذر ('/')
// عندما يزور شخص ما الصفحة الرئيسية، سيتم تنفيذ هذه الدالة
app.get('/', (req, res) => {
  res.send('Hello World!'); // إرسال استجابة نصية بسيطة
});

// 5. تشغيل الخادم للاستماع للطلبات على المنفذ المحدد
app.listen(port, () => {
  console.log(`Server is running at http://localhost:${port}`);
});
```

---
### ▶️ 4. تشغيل الخادم
الآن، عد إلى الطرفية وتأكد من أنك في مجلد `my-express-app`، ثم نفذ الأمر التالي:
```bash
node index.js
```
سترى الرسالة التالية في طرفيتك:
```
Server is running at http://localhost:3000
```
هذا يعني أن خادمك يعمل الآن! افتح متصفح الويب الخاص بك واذهب إلى العنوان `http://localhost:3000`. يجب أن ترى رسالة "Hello World!". لإيقاف الخادم، ارجع إلى الطرفية واضغط `Ctrl + C`.

---
