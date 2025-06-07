# الوحدة 4: المصفوفات والكائنات

## الدرس 3: الكائنات الحرفية (Object Literals)

---

🧠 **ماذا ستتعلم**
*	ما هي الكائنات في جافاسكريبت
*	كيفية إنشاء الكائنات باستخدام الكائنات الحرفية
*	كيفية الوصول إلى خصائص الكائن وتحديثها
*	الفرق بين طريقة الترميز بالنقطة (dot notation) والترميز بالأقواس (bracket notation)

---

🗂️ **1. ما هو الكائن؟**

الكائن هو مجموعة من أزواج المفتاح-القيمة (key-value pairs).
يُطلق على كل مفتاح اسم خاصية (property).
```javascript
let person = {
  name: "Alice",
  age: 25,
  isStudent: true
};
```
في هذا المثال:
*	`"name"` هو مفتاح، و `"Alice"` هي قيمته
*	`"age"` هو مفتاح، و `25` هي قيمته

---

🛠️ **2. إنشاء الكائنات (الكائنات الحرفية)**

تقوم بإنشاء كائن باستخدام الأقواس المعقوفة `{}` مع أزواج المفتاح-القيمة.
```javascript
let car = {
  brand: "Toyota",
  model: "Corolla",
  year: 2020
};
```
المفاتيح عادة ما تكون سلاسل نصية (بدون علامات اقتباس ما لم تكن هناك حاجة إليها).
يمكن أن تكون القيم أي نوع بيانات: سلسلة نصية، رقم، قيمة منطقية، مصفوفة، كائن، أو حتى دوال.

---

🔍 **3. الوصول إلى الخصائص**

✅ **الترميز بالنقطة (Dot Notation):**
```javascript
let user = {
  username: "coder123",
  score: 100
};

console.log(user.username); // الناتج: "coder123"
```

🔑 **الترميز بالأقواس (Bracket Notation):**
```javascript
console.log(user["score"]); // الناتج: 100
```
استخدم الترميز بالأقواس عندما:
*	يحتوي المفتاح على أحرف خاصة (مثل `"user-name"`)
*	يكون المفتاح مخزنًا في متغير
```javascript
let key = "username";
console.log(user[key]); // الناتج: "coder123"
```

---

✏️ **4. تحديث وإضافة الخصائص**

يمكنك تحديث الخصائص الموجودة أو إضافة خصائص جديدة:
```javascript
user.score = 200;
user.rank = "Gold";

console.log(user);
// الناتج: { username: "coder123", score: 200, rank: "Gold" }
```

---

❌ **5. حذف الخصائص**

قم بإزالة خاصية باستخدام الكلمة المفتاحية `delete`:
```javascript
delete user.rank;
console.log(user); // الناتج: { username: "coder123", score: 200 } (تم حذف rank)
```
*(Note: The exact output in the comment is more precise, so I've added it)*

---

🧪 **جرب بنفسك**
```javascript
let book = {
  title: "1984",
  author: "George Orwell",
  pages: 328
};

console.log(book.title);      // الناتج: "1984"
book.pages = 350;             // تحديث الصفحات
book.genre = "Dystopian";     // إضافة خاصية جديدة
delete book.author;           // إزالة المؤلف

console.log(book); // المتوقع أن يطبع: { title: "1984", pages: 350, genre: "Dystopian" }
```

---

🧠 **النقاط الرئيسية**
*	الكائنات تخزن أزواج المفتاح-القيمة.
*	استخدم الترميز بالنقطة أو الترميز بالأقواس للوصول إلى الخصائص.
*	يمكنك تحديث، إضافة، أو حذف الخصائص في أي وقت.
*	يمكن أن تكون قيم الكائن من أي نوع — حتى مصفوفات أو كائنات أخرى.

---