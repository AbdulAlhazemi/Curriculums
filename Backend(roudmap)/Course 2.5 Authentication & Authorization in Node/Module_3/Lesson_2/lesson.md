## 🔑 الوحدة 3: مواضيع متقدمة في الأمان

### 📘 الدرس 2: التحكم في الوصول القائم على الأدوار (RBAC)

#### 🧠 **ماذا ستتعلم**
* ما هو التحكم في الوصول القائم على الأدوار (Role-Based Access Control - RBAC).
* إعادة تأكيد الفرق بين المصادقة والتخويل.
* كيفية تصميم نظام أدوار بسيط (مثل `user` مقابل `admin`).
* كيفية تطبيق Middleware للتخويل في Express لحماية المسارات بناءً على أدوار المستخدمين.

---
### 🤔 1. ما بعد المصادقة: التخويل
المصادقة تجيب على سؤال "من أنت؟". لكن بمجرد أن نعرف أن المستخدم هو "أحمد"، هذا لا يخبرنا بأي شيء عن صلاحياته. هل "أحمد" مجرد مستخدم عادي أم هو مدير للنظام؟

هنا يأتي دور **التخويل (Authorization)**، الذي يجيب على سؤال "ماذا يمكنك أن تفعل؟". **RBAC** هو أحد أشهر وأبسط الأنماط لتطبيق التخويل.

**الفكرة:** بدلاً من تعيين صلاحيات لكل مستخدم على حدة (وهو أمر معقد جدًا)، نقوم بإنشاء "أدوار" (Roles) مثل `admin`, `editor`, `viewer`. نعطي الصلاحيات لهذه الأدوار، ثم نعين الأدوار للمستخدمين.

> **ببساطة:** في شركة، لا يتم إعطاء كل موظف مفتاحًا مخصصًا لكل غرفة يحتاجها. بدلاً من ذلك، هناك أدوار: "مدير"، "محاسب"، "موظف". مفتاح "المدير" يفتح جميع الأبواب. مفتاح "المحاسب" يفتح مكتب المالية فقط. أنت تحصل على المفتاح الذي يناسب دورك.

---
### ⚙️ 2. كيف يعمل التحكم في الوصول القائم على الأدوار؟
1.  **تعريف الأدوار:** حدد الأدوار المختلفة في تطبيقك (مثلاً `admin`, `member`).
2.  **تحديد الصلاحيات:** لكل دور، حدد ما هي الإجراءات المسموح بها (مثلاً، `admin` يمكنه حذف المستخدمين، بينما `member` لا يمكنه ذلك).
3.  **تعيين الأدوار للمستخدمين:** عند إنشاء مستخدم جديد، يتم تعيين دور له.
4.  **تضمين الدور في التوكن:** لتحقيق التخويل عديم الحالة، يجب تضمين دور المستخدم كجزء من حمولة (Payload) توكن JWT الخاص به.
    ```json
    {
      "id": 123,
      "username": "jameel",
      "role": "admin"
    }
    ```
5.  **التحقق من الدور:** عند كل طلب إلى مسار محمي، يقوم Middleware خاص بالتخويل بالتحقق من الدور الموجود في التوكن لتحديد ما إذا كان يجب السماح بالوصول أم لا.

---
### 🛡️ 3. تطبيق RBAC في Express
سنقوم بإنشاء Middleware للتخويل يكون مرنًا بما يكفي ليسمح لنا بتحديد الأدوار المسموح بها لكل مسار.

**المتطلب السابق:** نفترض أن Middleware المصادقة (من الدرس 7) قد تم تنفيذه بالفعل وأنه يضيف بيانات المستخدم المفككة من التوكن إلى `req.user`.

**مثال: Middleware للتخويل (`authorize.js`)**
هذه الدالة *تُرجع* دالة Middleware. هذا نمط شائع لجعل الـ Middleware قابلاً للتخصيص.
```javascript
// نمرر الأدوار المسموح بها كوسيطات
const authorize = (...allowedRoles) => {
  return (req, res, next) => {
    // نفترض أن المصادقة تمت وأن req.user موجود
    const userRole = req.user.role;
    
    // نتحقق مما إذا كان دور المستخدم مدرجًا في قائمة الأدوار المسموح بها
    if (allowedRoles.includes(userRole)) {
      next(); // مسموح، انتقل للتالي
    } else {
      // غير مسموح، أرسل خطأ "Forbidden"
      res.status(403).json({ message: "Forbidden: You do not have the right permissions." });
    }
  };
};

module.exports = authorize;
```
**استخدام الـ Middleware لحماية المسارات:**
```javascript
const authMiddleware = require('./authMiddleware'); // Middleware المصادقة
const authorize = require('./authorize'); // Middleware التخويل

// هذا المسار محمي للمستخدمين الذين لديهم دور 'admin' فقط
app.delete('/api/users/:id', authMiddleware, authorize('admin'), (req, res) => {
  // ... منطق حذف المستخدم
});

// هذا المسار محمي للمدراء والمحررين
app.put('/api/posts/:id', authMiddleware, authorize('admin', 'editor'), (req, res) => {
  // ... منطق تعديل المقال
});
```
---

