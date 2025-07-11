## 🚀 الوحدة 2: البرمجيات الوسيطة ودورة الطلب/الاستجابة

### 📘 الدرس 3: كائنات الطلب والاستجابة (The Req & Res Objects)

#### 🧠 **ماذا ستتعلم**
* الدور الأساسي لكائني الطلب (`req`) والاستجابة (`res`).
* الخصائص المفيدة في كائن `req` (مثل `params`, `query`, `body`, `headers`).
* الدوال المفيدة في كائن `res` (مثل `send`, `json`, `status`, `redirect`).
* كيفية ربط دوال الاستجابة معًا (Method Chaining).

---
### 🎯 1. قلب كل معالج: `req` و `res`
كل دالة معالج مسار (route handler) أو دالة برمجية وسيطة (middleware) في Express تستقبل كائنين رئيسيين:

1.  **`req` (كائن الطلب - Request):** يمثل طلب HTTP الوارد. يحتوي على جميع المعلومات التي أرسلها العميل، مثل عنوان URL، الترويسات، البيانات المرسلة، والمزيد. أنت تستخدمه **للحصول على** معلومات.
2.  **`res` (كائن الاستجابة - Response):** يمثل استجابة HTTP التي سيقوم تطبيق Express بإرسالها. أنت تستخدمه **لإرسال** المعلومات والبيانات مرة أخرى إلى العميل.

---
### 📥 2. كائن الطلب (`req`) بالتفصيل
يحتوي كائن `req` على العديد من الخصائص المفيدة لاستخلاص المعلومات من الطلب الوارد.

| الخاصية | الوصف | مثال |
| :--- | :--- | :--- |
| **`req.params`**| كائن يحتوي على معلمات المسار (Route Parameters). | في المسار `/users/:id`، `req.params.id` سيحتوي على قيمة `id`. |
| **`req.query`** | كائن يحتوي على سلاسل الاستعلام (Query Strings). | في `?sort=asc`، `req.query.sort` سيكون `"asc"`. |
| **`req.body`** | كائن يحتوي على البيانات المرسلة في جسم الطلب (عادةً مع `POST` أو `PUT`). | يتطلب Middleware مثل `express.json()` ليعمل. |
| **`req.method`**| يحدد فعل HTTP للطلب (`GET`, `POST`, إلخ). | `GET` |
| **`req.headers`**| كائن يحتوي على جميع ترويسات HTTP التي أرسلها العميل. | `req.headers['user-agent']` |

---
### 📤 3. كائن الاستجابة (`res`) بالتفصيل
يحتوي كائن `res` على دوال لإرسال الاستجابة إلى العميل. استدعاء أي من هذه الدوال (باستثناء `status`) ينهي دورة الطلب-الاستجابة.

| الدالة | الوصف |
| :--- | :--- |
| **`res.send([body])`**| ترسل استجابة HTTP. يمكن أن يكون الجسم نصًا، كائن HTML، أو JSON. |
| **`res.json([body])`**| ترسل استجابة بصيغة JSON. تقوم تلقائيًا بتعيين ترويسة `Content-Type` إلى `application/json`. **(الطريقة المفضلة للـ APIs)**. |
| **`res.status(code)`**| تحدد رمز حالة HTTP للاستجابة (مثل `200`, `404`, `500`). **لا ترسل الاستجابة بنفسها**، ولكنها تُرجع كائن `res` للسماح بالربط (chaining). |
| **`res.redirect(path)`**| تعيد توجيه طلب العميل إلى مسار أو URL آخر. |
| **`res.render(view)`** | (سنتعلمه لاحقًا) تستخدم مع محركات القوالب لعرض صفحة HTML ديناميكية. |

#### **ربط الدوال (Method Chaining)**
يمكنك ربط `res.status()` مع دوال الإرسال الأخرى في سطر واحد، وهو النمط الشائع جدًا في Express.
```javascript
// إرسال استجابة نجاح مع بيانات JSON
res.status(200).json({ message: 'Success', data: users });

// إرسال استجابة خطأ "غير موجود"
res.status(404).send('Sorry, user not found.');

// إرسال استجابة "تم الإنشاء بنجاح"
res.status(201).json({ message: 'User created successfully' });
```
---

