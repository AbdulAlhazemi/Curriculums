## 🟩 الوحدة 3: أساسيات Node.js

### 📘 الدرس 5: NPM (Node Package Manager) - إدارة تبعيات المشروع

#### 🧠 ماذا ستتعلم؟
* ما هو **NPM** ولماذا هو مهم في مشاريع Node.js.
* كيفية إنشاء ملف `package.json` وإدارته.
* كيف تثبت الحزم (packages) باستخدام `npm install`.
* فهم الفرق بين التبعيات العادية (**dependencies**) والتبعيات التطويرية (**devDependencies**).
* تشغيل السكريبتات (scripts) من `package.json`.

---
### 1. ما هو NPM؟
**NPM** هو مدير الحزم الخاص بـ Node.js. يسمح لك بسهولة تثبيت مكتبات وأدوات خارجية تحتاجها في مشروعك دون الحاجة لكتابة كل شيء بنفسك.

---
### 2. ملف package.json
هو الملف الذي يحتوي على بيانات المشروع مثل الاسم، الإصدار، التبعيات، وأوامر التشغيل.

يمكنك إنشاؤه باستخدام:
```bash
npm init
```
أو بشكل سريع، لتخطي جميع الأسئلة:
```bash
npm init -y
```

---
### 3. تثبيت الحزم
لتثبيت حزمة معينة (مثلاً **Express**، وهو إطار عمل لبناء تطبيقات الويب):
```bash
npm install express
```
سيتم إضافة هذه الحزمة تلقائيًا إلى قسم `dependencies` في ملف `package.json`.

---
### 4. التبعيات التطويرية (devDependencies)
هذه الحزم تُستخدم فقط أثناء التطوير ولا يتم تضمينها في النسخة النهائية من التطبيق، مثل أدوات اختبار الكود أو أدوات إعادة تشغيل الخادم تلقائيًا.

لتثبيت حزمة كـ `devDependency` (مثل **nodemon**):
```bash
npm install --save-dev nodemon
```

---
### 5. تشغيل السكريبتات (scripts)
يمكنك تعريف أوامر مخصصة لتشغيلها بسهولة عبر قسم `scripts` في ملف `package.json`:
```json
"scripts": {
  "start": "node app.js",
  "dev": "nodemon app.js"
}
```
لتشغيل الأمر `dev`:
```bash
npm run dev
```

---