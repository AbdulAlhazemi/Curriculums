## 🚀 الوحدة 3: بناء تطبيقات متكاملة

### 📘 الدرس 1: خدمة الملفات الثابتة (Serving Static Files)

#### 🧠 **ماذا ستتعلم**
* ما هي الملفات الثابتة في سياق تطبيقات الويب.
* كيفية استخدام الـ Middleware المدمج `express.static()`.
* كيفية تنظيم الملفات الثابتة في مجلد مخصص (مثل `public`).
* كيف يقوم المتصفح بطلب هذه الملفات من خادم Express.

---
### 📄 1. ما هي الملفات الثابتة؟
الملفات الثابتة (Static Files or Assets) هي الملفات التي يتم إرسالها إلى العميل (المتصفح) **كما هي**، دون أي تعديل أو معالجة من جانب الخادم. الخادم ببساطة يقرأ الملف من القرص الصلب ويرسله.

**أمثلة شائعة:**
* ملفات HTML
* أوراق أنماط CSS
* ملفات جافاسكريبت الخاصة بالعميل (Client-side JS)
* الصور (JPG, PNG, SVG)
* الخطوط (Fonts)

هذا يختلف عن المحتوى الديناميكي (مثل استجابة API) الذي يتم إنشاؤه بواسطة الخادم عند كل طلب.

---
### ⚙️ 2. استخدام `express.static`
يوفر Express دالة Middleware مدمجة اسمها `express.static` مصممة خصيصًا لخدمة الملفات الثابتة.

**كيف تعمل:**
تقوم بتحديد اسم مجلد يحتوي على ملفاتك الثابتة. عندما يصل طلب إلى الخادم، سيتحقق `express.static` مما إذا كان هناك ملف يطابق مسار الطلب داخل هذا المجلد.
* **إذا وجد الملف:** سيقوم بخدمته تلقائيًا وإرساله إلى العميل.
* **إذا لم يجد الملف:** سيتجاهل الطلب ويمرره إلى الـ Middleware أو المسارات التالية في السلسلة.

**الصيغة العامة:**
```javascript
app.use(express.static('directory_name'));
```
الاسم الأكثر شيوعًا لهذا المجلد هو `public`.

---
### 🛠️ 3. مثال عملي: إعداد مجلد `public`

#### **الخطوة 1: إنشاء المجلدات والملفات**
في جذر مشروعك، أنشئ مجلدًا جديدًا باسم `public`. بداخله، أنشئ الملفات التالية:
1.  **`public/index.html`:**
    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <title>My Static Site</title>
      <link rel="stylesheet" href="/style.css">
    </head>
    <body>
      <h1>Hello from a static HTML file!</h1>
    </body>
    </html>
    ```
2.  **`public/style.css`:**
    ```css
    body {
      background-color: #f0f0f0;
      font-family: sans-serif;
      color: #333;
    }
    ```

#### **الخطوة 2: إعداد Express**
في ملف `index.js` الخاص بك، أضف السطر التالي:
```javascript
const express = require('express');
const app = express();
const port = 3000;

// استخدم express.static لخدمة الملفات من مجلد 'public'
app.use(express.static('public'));

app.listen(port, () => {
  console.log(`Server listening at http://localhost:${port}`);
});
```

#### **الخطوة 3: التشغيل والاختبار**
1.  شغل الخادم: `node index.js`.
2.  افتح متصفحك واذهب إلى `http://localhost:3000`.

**ماذا حدث؟**
1.  طلب المتصفح المسار `/`.
2.  بحث `express.static` داخل مجلد `public` عن ملف افتراضي يطابق هذا المسار (وهو `index.html`).
3.  وجد `public/index.html` وأرسله إلى المتصفح.
4.  قرأ المتصفح ملف HTML ورأى الوسم `<link rel="stylesheet" href="/style.css">`، لذا أرسل طلبًا ثانيًا إلى الخادم للحصول على `/style.css`.
5.  مرة أخرى، بحث `express.static` ووجد `public/style.css` وأرسله.

---
