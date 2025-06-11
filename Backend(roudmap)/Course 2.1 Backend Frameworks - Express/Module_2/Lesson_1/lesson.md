## 🚀 الوحدة 2: البرمجيات الوسيطة ودورة الطلب/الاستجابة

### 📘 الدرس 1: البرمجيات الوسيطة (Middleware)

#### 🧠 **ماذا ستتعلم**
* ما هي البرمجيات الوسيطة (Middleware) وما هو دورها المحوري في Express.
* الهيكل الأساسي لدالة الـ Middleware (مع `req`, `res`, `next`).
* كيفية كتابة واستخدام Middleware مخصص.
* كيفية استخدام Middleware من طرف ثالث مثل `morgan` و `express.json`.

---
### 🔗 1. ما هي البرمجيات الوسيطة؟
البرمجيات الوسيطة هي **دوال** تعمل في نقطة ما **بين** استقبال الخادم للطلب (`Request`) وإرساله للاستجابة (`Response`). كل طلب في تطبيق Express يمر عبر سلسلة من هذه الدوال.

> **ببساطة:** تخيل خط تجميع في مصنع. الطلب (`req`) هو المنتج الذي يتحرك على الحزام الناقل. كل دالة Middleware هي محطة على هذا الخط تقوم بمهمة معينة: محطة تفحص المنتج (تسجيل الطلب)، محطة تضيف قطعة جديدة (إضافة بيانات للطلب)، محطة تغلفه (تحليل البيانات). بعد أن تنتهي كل محطة من عملها، تمرر المنتج إلى المحطة **التالية (`next`)**.

**ماذا يمكن أن تفعل الـ Middleware؟**
* تنفيذ أي كود برمجي.
* إجراء تغييرات على كائني الطلب (`req`) والاستجابة (`res`).
* إنهاء دورة الطلب-الاستجابة (عن طريق إرسال استجابة).
* استدعاء دالة الـ Middleware التالية في السلسلة (`next`).

---
### ✍️ 2. كتابة Middleware مخصص
دالة الـ Middleware تأخذ ثلاثة معاملات: `req`, `res`, و `next`.

* **`next()`:** هذا هو أهم جزء. يجب عليك استدعاء `next()` في نهاية دالتك لتمرير التحكم إلى الـ Middleware التالي في السلسلة. إذا لم تقم بذلك (أو لم ترسل استجابة)، سيبقى الطلب "معلقًا" ولن يكتمل أبدًا.

**مثال: Middleware بسيط لتسجيل وقت الطلب**
```javascript
const express = require('express');
const app = express();

// هذه دالة الـ Middleware الخاصة بنا
const requestLogger = (req, res, next) => {
  console.log(`[${new Date().toISOString()}] ${req.method} ${req.url}`);
  next(); // مهم جدًا: مرر التحكم للتالي!
};

// استخدام الـ Middleware على مستوى التطبيق (سيتم تنفيذه مع كل طلب)
app.use(requestLogger);

app.get('/', (req, res) => {
  res.send('Homepage');
});

app.get('/about', (req, res) => {
  res.send('About Us');
});

app.listen(3000, () => console.log('Server running on port 3000'));
```
الآن، كل طلب يصل إلى خادمك سيتم تسجيله أولاً في الطرفية بفضل الـ Middleware.

---
### 🧩 3. استخدام Middleware من طرف ثالث
لست مضطرًا لكتابة كل شيء بنفسك. مجتمع `npm` مليء بحزم Middleware جاهزة للمهام الشائعة.

#### **`morgan` - لتسجيل الطلبات**
`morgan` هو Middleware احترافي لتسجيل طلبات HTTP، يوفر تفاصيل وتنسيقات أكثر من المثال الذي كتبناه.
1.  **التثبيت:** `npm install morgan`
2.  **الاستخدام:**
    ```javascript
    const morgan = require('morgan');
    // ...
    // 'dev' هو تنسيق تسجيل شائع وبسيط
    app.use(morgan('dev'));
    ```

#### **`express.json()` - لتحليل بيانات JSON**
هذا هو واحد من أهم الـ Middleware. عندما يرسل العميل بيانات بصيغة JSON في جسم الطلب (مثل طلبات `POST` لإنشاء مورد)، يقوم هذا الـ Middleware بتحليلها ووضعها في `req.body` لتتمكن من استخدامها بسهولة.
1.  **الاستخدام:** (هذا الـ Middleware مدمج مع Express، لا حاجة لتثبيت شيء).
    ```javascript
    // يجب استخدام هذا الـ Middleware قبل أي مسار يحتاج لقراءة جسم الطلب
    app.use(express.json());

    app.post('/api/users', (req, res) => {
      // بفضل express.json()، يمكننا الآن الوصول إلى البيانات
      const newUser = req.body;
      console.log('Received new user:', newUser);
      res.status(201).send(`User named ${newUser.name} was created.`);
    });
    ```
---
