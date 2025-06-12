## 📐 الوحدة 1: مبادئ الكود النظيف وأنماط التصميم

### 📘 الدرس 1: كتابة الكود النظيف

#### 🧠 **ماذا ستتعلم**
* أهمية كتابة الكود النظيف وسهل القراءة.
* أفضل الممارسات لتسمية المتغيرات والدوال والكلاسات.
* فهم وتطبيق مبدأ **KISS (اجعله بسيطًا يا صاح)**.
* فهم وتطبيق مبدأ **DRY (لا تكرر نفسك)**.

---
### 🤔 1. لماذا نهتم بالكود النظيف؟
الحقيقة البسيطة هي أن المطورين يقضون وقتًا في **قراءة** الكود أكثر بكثير من الوقت الذي يقضونه في **كتابته**. الكود النظيف ليس موجهًا للحاسوب، بل هو موجه للمطورين الآخرين، ولنفسك في المستقبل.

* **فوائد الكود النظيف:**
    * **سهولة القراءة والفهم.**
    * **سهولة الصيانة والتصحيح (Debugging).**
    * **سهولة إضافة ميزات جديدة.**
    * **أخطاء برمجية أقل.**

> **ببساطة:** الكود النظيف يشبه ورشة عمل منظمة. يمكنك العثور على أدواتك بسرعة والعمل بكفاءة. أما الكود الفوضوي فهو ورشة عمل مبعثرة، حيث تقضي معظم وقتك في البحث عن الأدوات بدلاً من البناء.

---
### 🏷️ 2. التسمية الجيدة: مفتاح الوضوح
القاعدة الأساسية هي أن الاسم يجب أن **يكشف عن القصد**. اسم المتغير يجب أن يخبرك بما يحتويه، واسم الدالة يجب أن يخبرك بما تفعله.

| سيئ ❌ | جيد ✅ | الشرح |
| :--- | :--- | :--- |
| `let d;` | `let daysSinceLastLogin;`| كن واضحًا ومحددًا. تجنب الأسماء المختصرة الغامضة. |
| `function processData() {}` | `function filterActiveUsers() {}` | كن دقيقًا في وصف ما تفعله الدالة. |
| `const list = getUsers();`| `const users = getUsers();` | سمِّ المتغير بناءً على ما يمثله، وليس نوعه. |
| `let is_active_user;` | `let isActiveUser;` | استخدم صيغة `camelCase` في جافاسكريبت. |

---
### 💋 3. مبدأ KISS: اجعله بسيطًا يا صاح
**KISS** هو اختصار لـ **"Keep It Simple, Stupid"**. هذا المبدأ يدعو إلى أن البساطة يجب أن تكون هدفًا رئيسيًا في التصميم، ويجب تجنب التعقيد غير الضروري. الحل الأبسط غالبًا ما يكون هو الأفضل.

**مثال:**
```javascript
// سيئ: معقد وصعب القراءة
function getTitle(user) {
  return user.isLoggedIn ? (user.isAdmin ? "Admin Dashboard" : "User Dashboard") : "Login Page";
}

// جيد: أبسط وأكثر وضوحًا
function getTitle(user) {
  if (!user.isLoggedIn) {
    return "Login Page";
  }
  if (user.isAdmin) {
    return "Admin Dashboard";
  }
  return "User Dashboard";
}
```

---
### 💧 4. مبدأ DRY: لا تكرر نفسك
**DRY** هو اختصار لـ **"Don't Repeat Yourself"**. هذا المبدأ ينص على أن كل جزء من المنطق في نظامك يجب أن يكون له تمثيل واحد فقط وغير غامض.

* **المشكلة:** نسخ ولصق الكود هو علامة خطر كبيرة. إذا كان لديك نفس الكود في مكانين وقمت بتعديل أحدهما، فمن السهل جدًا أن تنسى تعديل الآخر، مما يؤدي إلى أخطاء.
* **الحل:** قم بتجريد المنطق المكرر في دالة قابلة لإعادة الاستخدام.

**مثال:**
```javascript
// سيئ: تكرار منطق التحقق من البريد الإلكتروني
function createUser(email, password) {
  if (email.length === 0 || !email.includes('@')) {
    throw new Error('Invalid email for new user.');
  }
  // ...
}
function updateUser(userId, email) {
  if (email.length === 0 || !email.includes('@')) {
    throw new Error('Invalid email for update.');
  }
  // ...
}


// جيد: تطبيق مبدأ DRY
function isValidEmail(email) {
  return email && email.includes('@');
}
function createUser(email, password) {
  if (!isValidEmail(email)) {
    throw new Error('Invalid email for new user.');
  }
  // ...
}
function updateUser(userId, email) {
  if (!isValidEmail(email)) {
    throw new Error('Invalid email for update.');
  }
  // ...
}
```

---
