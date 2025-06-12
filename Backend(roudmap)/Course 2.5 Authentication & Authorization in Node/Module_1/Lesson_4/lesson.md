## 🔑 الوحدة 1: أساسيات المصادقة والتخويل

### 📘 الدرس 4: تطبيق المصادقة بالجلسات مع Express

#### 🧠 **ماذا ستتعلم**
* كيفية تثبيت وإعداد الـ Middleware `express-session`.
* كيفية إنشاء جلسة مستخدم عند تسجيل الدخول الناجح.
* كيفية الوصول إلى بيانات الجلسة في الطلبات اللاحقة لحماية المسارات.
* كيفية تدمير الجلسة عند تسجيل الخروج.
* أهمية خيار `secret` في إعدادات الجلسة.

---
### ⚙️ 1. الأداة: `express-session`
`express-session` هي حزمة Middleware تقوم بكل العمل الشاق لإدارة الجلسات نيابة عنك. هي مسؤولة عن:
* إنشاء معرفات جلسة فريدة.
* إنشاء وإرسال الكوكي إلى المتصفح.
* قراءة الكوكي من الطلبات الواردة.
* إنشاء كائن `req.session` يمكنك استخدامه لتخزين واسترجاع بيانات الجلسة.

> **ملاحظة:** بشكل افتراضي، تقوم `express-session` بتخزين الجلسات في ذاكرة الخادم. هذا مناسب للتطوير، ولكنه غير مناسب للإنتاج (لأن البيانات ستضيع عند إعادة تشغيل الخادم). في تطبيقات الإنتاج، يتم استخدام مخزن جلسات خارجي مثل قاعدة بيانات أو Redis.

---
### 🔧 2. الإعداد والتهيئة

#### **الخطوة 1: التثبيت**
```bash
npm install express-session
```

#### **الخطوة 2: الإعداد في `index.js`**
يجب عليك استخدام الـ Middleware في تطبيق Express الخاص بك وتمرير كائن إعدادات له.
```javascript
const session = require('express-session');

app.use(session({
  // مفتاح سري يستخدم لتوقيع كوكي معرف الجلسة. يجب أن يكون سلسلة نصية طويلة وعشوائية.
  secret: 'a-very-long-and-random-secret-string', 
  
  // يمنع إعادة حفظ الجلسة إذا لم تتغير. يحسن الأداء.
  resave: false,
  
  // يمنع إنشاء جلسة لمستخدم لم يقم بتعديلها (مثل مستخدم زائر).
  saveUninitialized: false,
  
  // إعدادات الكوكي نفسه
  cookie: { secure: false, maxAge: 60000 } // في الإنتاج، يجب أن يكون secure: true
}));
```
---
### 🔐 3. تطبيق دورة تسجيل الدخول والخروج

#### **أ. مسار تسجيل الدخول (`POST /login`)**
عندما يقوم المستخدم بتسجيل الدخول بنجاح، نقوم بإنشاء الجلسة عن طريق إضافة بيانات إلى الكائن `req.session`.
```javascript
app.post('/login', (req, res) => {
  const { username, password } = req.body;

  // في تطبيق حقيقي، ستقوم بالتحقق من البيانات مقابل قاعدة البيانات
  if (username === 'admin' && password === 'password123') {
    // إنشاء الجلسة عن طريق تعيين خاصية على req.session
    req.session.user = { id: 1, username: 'admin' };
    res.send('Login successful');
  } else {
    res.status(401).send('Invalid credentials');
  }
});
```
#### **ب. حماية مسار (`GET /profile`)**
الآن، يمكننا حماية المسارات عن طريق إنشاء Middleware يتحقق مما إذا كانت `req.session.user` موجودة.
```javascript
// Middleware للتحقق من المصادقة
const checkAuth = (req, res, next) => {
  if (req.session.user) {
    next(); // المستخدم مصادق عليه، اسمح له بالمرور
  } else {
    res.status(401).send('You must be logged in to view this page.');
  }
};

// استخدام الـ Middleware لحماية هذا المسار
app.get('/profile', checkAuth, (req, res) => {
  res.send(`Welcome back, ${req.session.user.username}!`);
});
```

#### **ج. مسار تسجيل الخروج (`POST /logout`)**
لتسجيل الخروج، نقوم بتدمير الجلسة من جانب الخادم باستخدام `req.session.destroy()`.
```javascript
app.post('/logout', (req, res) => {
  req.session.destroy(err => {
    if (err) {
      return res.status(500).send('Could not log out.');
    }
    // مسح الكوكي من المتصفح أيضًا (اختياري)
    res.clearCookie('connect.sid'); // connect.sid هو الاسم الافتراضي لكوكي الجلسة
    res.send('Logout successful');
  });
});
```
---
