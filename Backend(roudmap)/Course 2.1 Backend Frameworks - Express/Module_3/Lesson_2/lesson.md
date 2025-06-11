## 🚀 الوحدة 3: بناء تطبيقات متكاملة

### 📘 الدرس 9: هيكلة تطبيقات Express (Structuring Express Applications)

#### 🧠 **ماذا ستتعلم**
* لماذا هيكلة التطبيقات الكبيرة أمر ضروري.
* ما هو `express.Router` وكيف يساعد في تنظيم المسارات.
* كيفية فصل المسارات (Routes) والمتحكمات (Controllers) في ملفات منفصلة.
* مقدمة في نمط MVC (Model-View-Controller) وتطبيقه في APIs.

---
### 🤔 1. المشكلة: كل شيء في ملف واحد
عندما بدأنا، كان وضع كل المسارات في ملف `index.js` واحد أمرًا سهلاً. لكن تخيل تطبيقًا حقيقيًا يحتوي على عشرات المسارات للمستخدمين، المنتجات، الطلبات، والتعليقات. سيصبح ملف `index.js` ضخمًا جدًا، فوضويًا، وصعب الصيانة.

**التحديات:**
* **صعوبة القراءة:** آلاف الأسطر من الكود في ملف واحد.
* **صعوبة الصيانة:** أي تغيير صغير قد يؤثر على أجزاء أخرى من التطبيق.
* **صعوبة العمل الجماعي:** يصبح من الصعب على عدة مطورين العمل على نفس الملف في وقت واحد.

---
###  çözüm 2. الحل: `express.Router`
`express.Router` هو الحل الذي يقدمه Express لهذه المشكلة. إنه يعمل كـ **"تطبيق Express مصغّر"** ومنفصل. يمكنك استخدامه لتجميع المسارات المتعلقة بمورد معين (مثل كل ما يتعلق بالمستخدمين) في ملف خاص بها، ثم "تركيب" (mount) هذا الراوتر على مسار معين في تطبيقك الرئيسي.

> **ببساطة:** تخيل أن تطبيقك الرئيسي (`app`) هو **متجر كبير (Mall)**. كل `Router` هو **قسم متخصص** داخل هذا المتجر (مثل قسم الإلكترونيات، قسم الملابس). كل قسم له ممراته ومداخله الخاصة (المسارات)، ولكنه في النهاية جزء من المتجر الكبير.

---
### 🛠️ 3. التطبيق العملي: فصل المسارات

#### **الخطوة 1: إنشاء مجلد للمسارات**
في مشروعك، أنشئ مجلدًا جديدًا باسم `routes`.

#### **الخطوة 2: إنشاء ملف مسار للمستخدمين (`routes/userRoutes.js`)**
```javascript
const express = require('express');
// 1. إنشاء نسخة من الراوتر
const router = express.Router();

// 2. تعريف المسارات على الراوتر بدلاً من app
// ملاحظة: المسار '/' هنا يعني '/users/' لأننا سنقوم بتركيبه على هذا المسار
router.get('/', (req, res) => {
  res.send('Get a list of all users');
});

// المسار '/:id' هنا يعني '/users/:id'
router.get('/:id', (req, res) => {
  res.send(`Get details for user with ID ${req.params.id}`);
});

// 3. تصدير الراوتر لكي نتمكن من استخدامه في الملف الرئيسي
module.exports = router;
```

#### **الخطوة 3: استخدام (تركيب) الراوتر في `index.js`**
```javascript
const express = require('express');
const app = express();
const port = 3000;

// 1. استيراد ملف مسارات المستخدمين
const userRoutes = require('./routes/userRoutes');

// 2. تركيب الراوتر على مسار أساسي
// أي طلب يبدأ بـ /users سيتم توجيهه إلى userRoutes
app.use('/users', userRoutes);

// يمكنك إضافة مسارات أخرى هنا، مثل مسارات المنتجات
// const productRoutes = require('./routes/productRoutes');
// app.use('/products', productRoutes);

app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```
بهذه الطريقة، أصبح ملف `index.js` نظيفًا ومسؤوليته فقط تجميع أجزاء التطبيق، بينما تم عزل منطق مسارات المستخدمين في ملف خاص به.

---
### 🕹️ 4. فصل المنطق: نمط المتحكمات (Controllers)
لزيادة التنظيم، يمكننا أن نأخذ خطوة إضافية. بدلاً من كتابة منطق كل مسار داخل ملف الراوتر، يمكننا فصله في ملفات خاصة تسمى **المتحكمات (Controllers)**.

* **المسار (Route):** وظيفته فقط تحديد نقطة النهاية (endpoint) وربطها بدالة متحكم.
* **المتحكم (Controller):** يحتوي على المنطق الفعلي الذي يتم تنفيذه عند طلب المسار.

**مثال: `controllers/userController.js`**
```javascript
const getAllUsers = (req, res) => {
  // منطق جلب المستخدمين من قاعدة البيانات
  res.send('Get a list of all users from controller');
};

const getUserById = (req, res) => {
  const userId = req.params.id;
  // منطق جلب مستخدم واحد
  res.send(`Get details for user with ID ${userId} from controller`);
};

module.exports = {
  getAllUsers,
  getUserById,
};
```
**تحديث `routes/userRoutes.js`:**
```javascript
const express = require('express');
const router = express.Router();
const userController = require('../controllers/userController'); // استيراد المتحكم

// ربط المسارات مباشرة بدوال المتحكم
router.get('/', userController.getAllUsers);
router.get('/:id', userController.getUserById);

module.exports = router;
```
الآن أصبح كل شيء منظمًا تمامًا ومفصولاً حسب وظيفته.

---
