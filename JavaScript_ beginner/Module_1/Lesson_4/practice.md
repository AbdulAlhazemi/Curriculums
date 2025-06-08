## 🧪 تحدي تدريبي: أنواع البيانات في JavaScript

### 🎯 التحدي:

في محرر JavaScript الخاص بك:

1. قم بالإعلان عن **خمسة متغيرات**، كل واحد بنوع بيانات مختلف:  
   - String (نص)  
   - Number (رقم)  
   - Boolean (قيمة منطقية)  
   - Null (قيمة فارغة)  
   - Undefined (غير معرّف)

2. اطبع **قيمة كل متغير** مع **نوعه** باستخدام `()console.log` و `typeof`.

3. قم بتغيير قيمة المتغير `null` ليحمل **قيمة حقيقية** (مثل رقم أو نص)، ثم اطبعه مرة أخرى مع نوعه.

---

### 💡 تلميحات:

- يمكنك استخدام `let` لتعريف المتغيرات القابلة للتغيير.
- استخدم `typeof` لمعرفة نوع المتغير.
- يمكن طباعة النوع والقيمة معًا هكذا:

  ```javascript
  console.log(typeof myVar, myVar);
  ```
✅ الحل النموذجي:
```javascript
let myString = "Hello";
let myNumber = 42;
let myBoolean = true;
let myNull = null;
let myUndefined;

console.log(typeof myString, myString);      // string
console.log(typeof myNumber, myNumber);      // number
console.log(typeof myBoolean, myBoolean);    // boolean
console.log(typeof myNull, myNull);          // object (سلوك معروف في JavaScript)
console.log(typeof myUndefined, myUndefined); // undefined

// تحديث قيمة null
myNull = "Now I have a value!";
console.log(typeof myNull, myNull);          // string
```
