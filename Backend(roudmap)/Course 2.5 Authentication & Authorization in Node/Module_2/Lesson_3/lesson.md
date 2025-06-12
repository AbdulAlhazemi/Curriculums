## 🔑 الوحدة 2: المصادقة القائمة على التوكن (Token-Based Authentication)

### 📘 الدرس 3: تطبيق JWT مع Node.js و Express

#### 🧠 **ماذا ستتعلم**
* كيفية استخدام حزمة `jsonwebtoken` الشهيرة في Node.js.
* كيفية إنشاء (توقيع) توكن JWT جديد عند تسجيل دخول ناجح.
* كيفية كتابة Middleware للتحقق من صحة التوكن في الطلبات الواردة.
* كيفية حماية المسارات (Routes) باستخدام هذا الـ Middleware.

---
### 🧰 1. الأداة: حزمة `jsonwebtoken`
لست بحاجة إلى بناء منطق JWT من الصفر. حزمة `jsonwebtoken` هي المعيار الفعلي في بيئة Node.js للتعامل مع JWTs بسهولة وأمان.

**الخطوة الأولى: التثبيت**
في مشروع Express الخاص بك، قم بتثبيت الحزمة:
```bash
npm install jsonwebtoken
```

---
### ✍️ 2. إنشاء وتوقيع التوكن (عند تسجيل الدخول)
يتم إنشاء التوكن بعد أن يتحقق الخادم من صحة بيانات اعتماد المستخدم (مثل اسم المستخدم وكلمة المرور). نستخدم دالة `jwt.sign()` لهذا الغرض.

* **دالة `jwt.sign(payload, secretKey, options)`:**
    * `payload`: كائن جافاسكريبت يحتوي على البيانات التي تريد وضعها في التوكن (مثل `userId`).
    * `secretKey`: مفتاح سري لا يعرفه أحد سوى الخادم. يستخدم لتوقيع التوكن. **يجب أن يكون معقدًا ويتم تخزينه كمتغير بيئة (`process.env.JWT_SECRET`)**.
    * `options`: كائن إعدادات إضافية، أهمها `expiresIn` لتحديد مدة صلاحية التوكن (مثل `'1h'`, `'7d'`).

**مثال: مسار تسجيل الدخول**
```javascript
const jwt = require('jsonwebtoken');

app.post('/login', (req, res) => {
  // 1. تحقق من اسم المستخدم وكلمة المرور (هنا مثال وهمي)
  const { username, password } = req.body;
  if (username !== 'admin' || password !== 'password123') {
    return res.status(401).send('Invalid credentials');
  }

  // 2. إذا كانت البيانات صحيحة، أنشئ الحمولة (Payload)
  const userPayload = { id: 1, username: 'admin', role: 'administrator' };
  
  // 3. قم بتوقيع التوكن
  // في تطبيق حقيقي، يجب أن يأتي المفتاح السري من متغيرات البيئة
  const accessToken = jwt.sign(userPayload, 'your_super_secret_key', { expiresIn: '1h' });

  // 4. أرسل التوكن إلى العميل
  res.json({ accessToken: accessToken });
});
```

---
### 🛡️ 3. التحقق من التوكن (حماية المسارات)
الآن، سنكتب Middleware للتحقق من التوكن في كل طلب يصل إلى مسار محمي.

* **دالة `jwt.verify(token, secretKey, callback)`:**
    * تأخذ التوكن والمفتاح السري.
    * تستدعي الـ callback مع خطأ (`err`) إذا كان التوكن غير صالح (توقيع خاطئ، منتهي الصلاحية، إلخ)، أو مع الحمولة المفككة (`decodedPayload`) إذا كان صالحًا.

**مثال: Middleware للمصادقة**
```javascript
const authMiddleware = (req, res, next) => {
  // 1. احصل على الترويسة
  const authHeader = req.headers['authorization'];
  
  // 2. احصل على التوكن (بعد كلمة "Bearer ")
  const token = authHeader && authHeader.split(' ')[1];

  // إذا لم يكن هناك توكن، أرسل خطأ
  if (token == null) return res.sendStatus(401); // Unauthorized

  // 3. تحقق من صحة التوكن
  jwt.verify(token, 'your_super_secret_key', (err, user) => {
    if (err) return res.sendStatus(403); // Forbidden (invalid token)
    
    // 4. إذا كان التوكن صالحًا، أضف الحمولة إلى كائن الطلب
    req.user = user;
    
    // 5. انتقل إلى الـ Middleware أو المسار التالي
    next();
  });
};
```
---
### ⚙️ 4. استخدام الـ Middleware لحماية المسارات
الآن ببساطة نضع `authMiddleware` قبل أي معالج مسار نريد حمايته.
```javascript
// هذا المسار محمي الآن
app.get('/api/dashboard', authMiddleware, (req, res) => {
  // بفضل الـ Middleware، نحن نعرف أن req.user موجود وصالح
  res.json({
    message: `Welcome to the dashboard, ${req.user.username}!`,
    userData: req.user
  });
});

// هذا المسار عام ومتاح للجميع
app.get('/', (req, res) => {
  res.send('This is the public homepage.');
});
```
---
