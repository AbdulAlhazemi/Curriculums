## 🟩 الوحدة 3: أساسيات Node.js

### 📘 الدرس 8: إدارة التبعيات باستخدام NPM (Node Package Manager) - مراجعة

#### 🧠 ماذا ستتعلم؟
* ما هو **NPM** ولماذا هو جزء أساسي من Node.js.
* كيفية تثبيت، حذف، وتحديث الحزم (Packages).
* الفرق بين التبعيات `dependencies` و `devDependencies`.
* كيفية قراءة وفهم محتوى ملف `package.json`.
* تشغيل الأوامر والسكريبتات داخل المشروع.

***

### 1. ما هو NPM؟
**NPM** هو **مدير الحزم الرسمي لـ Node.js**. يسمح لك بتثبيت مكتبات وأدوات جاهزة، وتنظيم التبعيات في مشروعك بسهولة.

***

### 2. إنشاء ملف `package.json`
لإنشاء الملف بسرعة وتخطي الأسئلة:
```bash
npm init -y
```
سيُنتج ملفًا يحتوي على معلومات المشروع الأساسية:
```json
{
  "name": "my-app",
  "version": "1.0.0",
  "main": "index.js",
  "dependencies": {},
  "scripts": {}
}
```

***

### 3. تثبيت الحزم

* **تثبيت تبعية عادية** (مكتبة يحتاجها التطبيق ليعمل):
    ```bash
    npm install express
    ```
    تُضاف إلى قسم `dependencies` في `package.json`:
    ```json
    "dependencies": {
      "express": "^4.18.2"
    }
    ```

* **تثبيت تبعية تطويرية** (أداة تساعدك أثناء البرمجة فقط):
    ```bash
    npm install --save-dev nodemon
    ```
    تُضاف إلى قسم `devDependencies`:
    ```json
    "devDependencies": {
      "nodemon": "^2.0.22"
    }
    ```

***

### 4. تشغيل السكريبتات
يمكنك تعريف أوامر مخصصة في `package.json` لتسهيل تشغيل المهام المتكررة.
```json
"scripts": {
  "start": "node app.js",
  "dev": "nodemon app.js"
}
```
لتشغيلها، استخدم الأمر:
```bash
npm run dev
```

***

### 5. تحديث أو حذف الحزم

* **لتحديث الحزم** إلى أحدث إصدار متوافق:
    ```bash
    npm update
    ```
* **لحذف حزمة** من المشروع:
    ```bash
    npm uninstall express
    ```

***