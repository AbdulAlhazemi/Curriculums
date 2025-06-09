# الوحدة 3: دوال المصفوفات المتقدمة

## الدرس 5: ترتيب وعكس المصفوفات


🧠 **ماذا ستتعلم**
*	كيفية ترتيب المصفوفات أبجديًا ورقميًا
*	كيفية عكس ترتيب المصفوفات
*	كيفية كتابة منطق ترتيب مخصص باستخدام دالة مقارنة (compare function)

---

🔢 **1. ترتيب السلاسل النصية أبجديًا**

تقوم دالة `()sort.` في جافاسكريبت بإعادة ترتيب عناصر المصفوفة في مكانها (in place).

مثال:
```javascript
const names = ["Charlie", "Alice", "Bob"];

names.sort();
console.log(names); // الناتج: ["Alice", "Bob", "Charlie"]
```
⚠️ دالة `()sort.` تعدل المصفوفة الأصلية.

---

🔢 **2. ترتيب الأرقام — انتبه!**

تتعامل دالة `()sort.` مع الأرقام كسلاسل نصية بشكل افتراضي، لذا قد يؤدي ذلك إلى نتائج خاطئة:
```javascript
const nums = [3, 20, 100, 5];

nums.sort();
console.log(nums); // الناتج: [100, 20, 3, 5] ❌
```

✅ استخدم دالة مقارنة لإصلاح ذلك:
```javascript
nums.sort((a, b) => a - b);
console.log(nums); // الناتج: [3, 5, 20, 100]
```

---

↩️ **3. عكس ترتيب المصفوفات**

استخدم `()reverse.` لعكس الترتيب:
```javascript
const letters = ["a", "b", "c"];
letters.reverse();
console.log(letters); // الناتج: ["c", "b", "a"]
```

🔁 دمج `()sort.` و `()reverse.`:
```javascript
// لنفترض أن nums هي [3, 5, 20, 100] من المثال السابق
nums.sort((a, b) => a - b).reverse(); // ترتيب تنازلي (سيصبح: [100, 20, 5, 3])
```

---

🔧 **4. ترتيب الكائنات حسب الخاصية**

رتب مصفوفة من الكائنات حسب مفتاح مثل `age`:
```javascript
const users = [
  { name: "Alice", age: 32 },
  { name: "Bob", age: 25 },
  { name: "Carol", age: 40 }
];

users.sort((a, b) => a.age - b.age);
console.log(users);
// الناتج المتوقع:
// [
//   { name: "Bob", age: 25 },
//   { name: "Alice", age: 32 },
//   { name: "Carol", age: 40 }
// ]
```

ترتيب أبجدي حسب الاسم:
```javascript
users.sort((a, b) => a.name.localeCompare(b.name));
// console.log(users); // ستكون المصفوفة users الآن مرتبة حسب الاسم
```

---

🧠 **النقاط الرئيسية**
*	استخدم `()sort.` مع دالة مقارنة للأرقام أو للترتيب المخصص.
*	استخدم `()reverse.` لعكس ترتيب أي مصفوفة.
*	رتب الكائنات باستخدام مقارنات الخصائص و `()localeCompare.` للسلاسل النصية.

---