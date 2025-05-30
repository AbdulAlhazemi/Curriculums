# الوحدة 4: المصفوفات والكائنات

## الدرس 4: الوصول إلى الخصائص وتعديلها

---

🧠 **ماذا ستتعلم**
*	كيفية الوصول إلى خصائص الكائن باستخدام ترميزات مختلفة
*	كيفية تحديث القيم الموجودة
*	كيفية إضافة خصائص جديدة
*	كيفية استخدام المتغيرات كمفاتيح مع الترميز بالأقواس

---

🔍 **1. الوصول إلى الخصائص**

✅ **الترميز بالنقطة (Dot Notation)**

استخدم الترميز بالنقطة عندما تعرف اسم الخاصية بالضبط.
```javascript
let user = {
  name: "Lara",
  age: 30
};

console.log(user.name); // الناتج: "Lara"
```

🔑 **الترميز بالأقواس (Bracket Notation)**

استخدم الترميز بالأقواس عندما:
*	يكون اسم الخاصية مخزنًا في متغير
*	يحتوي اسم الخاصية على مسافات أو أحرف خاصة
```javascript
let key = "age";
console.log(user[key]); // الناتج: 30

let person = {
  "first name": "Sam"
};
console.log(person["first name"]); // الناتج: "Sam"
```

---

✏️ **2. تعديل الخصائص الموجودة**

يمكنك تحديث القيم تمامًا مثل المتغيرات:
```javascript
user.age = 31;
user["name"] = "Lara Smith";

console.log(user);
// الناتج: { name: "Lara Smith", age: 31 }
```

---

➕ **3. إضافة خصائص جديدة**

إذا لم تكن الخاصية موجودة، فإن إسناد قيمة إليها ينشئها:
```javascript
user.country = "USA";
user["isAdmin"] = false;

console.log(user);
// الناتج: { name: "Lara Smith", age: 31, country: "USA", isAdmin: false }
```

---

❓ **4. التحقق من وجود الخاصية**

استخدم المعامل `in` أو الدالة `hasOwnProperty()`:
```javascript
console.log("age" in user); // الناتج: true
console.log(user.hasOwnProperty("email")); // الناتج: false
```

---

🧪 **جرب بنفسك**
```javascript
let product = {
  name: "Laptop",
  price: 999
};

product.price = 899;          // تحديث السعر
product["inStock"] = true;    // إضافة خاصية جديدة
let key = "name";
console.log(product[key]);    // الناتج: "Laptop"

console.log(product); // الناتج المتوقع: { name: "Laptop", price: 899, inStock: true }
```

---

🧠 **النقاط الرئيسية**
*	استخدم الترميز بالنقطة أو الترميز بالأقواس للوصول إلى خصائص الكائن.
*	الترميز بالنقطة أبسط؛ الترميز بالأقواس أكثر مرونة.
*	إسناد قيمة لمفتاح غير موجود يضيفه.
*	استخدم `"key" in object` أو `object.hasOwnProperty("key")` للتحقق من الوجود.


---