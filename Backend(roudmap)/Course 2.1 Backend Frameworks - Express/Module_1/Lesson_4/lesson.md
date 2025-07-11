## 🚀 الوحدة 1: أساسيات Express.js

### 📘 الدرس 4: معلمات المسار وسلاسل الاستعلام (Route Params & Query Strings)

#### 🧠 **ماذا ستتعلم**
* ما هي معلمات المسار (Route Parameters) وكيفية تعريفها والوصول إليها.
* ما هي سلاسل الاستعلام (Query Strings) وكيفية الوصول إليها.
* الفرق الرئيسي بينهما ومتى تستخدم كل نوع.

---
### 🤔 1. الحاجة إلى مسارات ديناميكية
في الدرس السابق، أنشأنا مسارات ثابتة مثل `/products` و `/products/1`. لكن من غير العملي إنشاء مسار جديد لكل منتج في متجرك. نحتاج إلى طريقة لإنشاء مسار "قالب" واحد يمكنه التعامل مع طلبات لآلاف المنتجات المختلفة. هذا ما تسمح به المسارات الديناميكية.

هناك طريقتان رئيسيتان لتمرير بيانات ديناميكية عبر عنوان URL: معلمات المسار وسلاسل الاستعلام.

---
### 🛣️ 2. الطريقة الأولى: معلمات المسار (Route Parameters)
معلمات المسار هي أجزاء من عنوان URL تستخدم لالتقاط قيم محددة. يتم تعريفها بوضع نقطتين رأسيتين (`:`) قبل اسمها.

* **حالة الاستخدام:** مثالية لتحديد **مورد معين ومطلوب**. المسار لا يكون له معنى بدونها.
* **الوصول إليها:** يوفر Express هذه المعلمات في الكائن `req.params`.

**مثال:**
لنرَ كيف ننشئ مسارًا واحدًا لجلب أي مستخدم بمعرف فريد.
```javascript
// هذا المسار سيتطابق مع /users/1, /users/abc, /users/507, etc.
app.get('/users/:id', (req, res) => {
  // للوصول إلى قيمة 'id'، نستخدم req.params.id
  const userId = req.params.id;
  res.send(`Fetching profile for user with ID: ${userId}`);
});
```
**للاختبار:** اذهب إلى `http://localhost:3000/users/123` في متصفحك. سترى الرسالة "Fetching profile for user with ID: 123".

---
### ❓ 3. الطريقة الثانية: سلاسل الاستعلام (Query Strings)
سلاسل الاستعلام هي مجموعة من أزواج المفتاح-القيمة التي تتم إضافتها إلى نهاية عنوان URL. تبدأ بعلامة استفهام (`?`) ويتم الفصل بين الأزواج بعلامة العطف (`&`).

* **حالة الاستخدام:** مثالية للمعلومات **الاختيارية**، مثل الفلترة، الترتيب، أو تحديد رقم الصفحة.
* **الوصول إليها:** يوفر Express هذه القيم في الكائن `req.query`.

**مثال:**
لنرَ كيف يمكننا فلترة نتائج البحث.
```javascript
// هذا المسار سيتعامل مع URL مثل: /search?keyword=express&limit=10
app.get('/search', (req, res) => {
  const keyword = req.query.keyword;
  const limit = req.query.limit;

  res.send(`Searching for "${keyword}" with a limit of ${limit} results.`);
});
```
**للاختبار:** اذهب إلى `http://localhost:3000/search?keyword=nodejs&limit=5`.

---
### ⚖️ 4. متى نستخدم كلًا منهما؟

| | معلمات المسار (`/products/:id`) | سلاسل الاستعلام (`/products?sort=price`) |
| :--- | :--- | :--- |
| **الغرض** | تحديد مورد **مطلوب** وفريد. | تمرير بيانات **اختيارية** أو خيارات فلترة/ترتيب. |
| **مثال** | جلب مستخدم معين، مقال معين، منتج معين. | فلترة المنتجات حسب الفئة، ترتيب النتائج، تحديد رقم الصفحة. |
| **الوصول** | `req.params` | `req.query` |

---
