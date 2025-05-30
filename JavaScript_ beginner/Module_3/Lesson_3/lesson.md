# الوحدة 3: الدوال (Functions)

## الدرس 3: القيم المُرجعة (Return Values)

🧠 **ماذا ستتعلم**
*	ماذا تفعل الكلمة المفتاحية `return`
*	كيفية إرجاع قيمة من دالة
*	كيفية تخزين واستخدام القيم المُرجعة
*	الفرق بين `console.log()` و `return`

---

🔙 **1. ما هي القيمة المُرجعة؟**

يمكن للدالة أن تُرجع قيمة إلى المكان الذي تم استدعاؤها منه. تقوم بذلك باستخدام الكلمة المفتاحية `return`.

مثال:
```javascript
function add(a, b) {
  return a + b;
}

let sum = add(3, 4);
console.log(sum); // الناتج: 7
```
*	الدالة تُرجع `a + b`
*	يتم تخزين تلك النتيجة في المتغير `sum`

---

🚫 **2. بدون `Return`**

إذا لم تستخدم `return`، فإن الدالة تُرجع `undefined` بشكل افتراضي.
```javascript
function greet(name) {
  console.log("Hello, " + name);
}

let message = greet("Alex");
console.log(message); // الناتج: undefined
```
على الرغم من أنها تطبع شيئًا، إلا أنها لا تُرجع أي شيء، لذا فإن `message` هي `undefined`.

---

🪄 **3. إرجاع قيمة مقابل طباعة قيمة**

| `console.log()`                  | `return`                               |
| :------------------------------- | :------------------------------------- |
| تطبع على الشاشة                  | تُرسل قيمة مرة أخرى إلى المستدعي        |
| لتصحيح الأخطاء/الإخراج           | لاستخدام النتائج في الكود              |
| لا تخزن البيانات                 | تمكنك من استخدام القيمة لاحقًا         |

---

⛔ **4. `Return` المبكرة تُنهي الدالة**

عندما تصل الدالة إلى جملة `return`، فإنها تخرج فورًا.
```javascript
function checkAge(age) {
  if (age < 18) {
    return "Too young!";
  }
  return "Access granted.";
}

console.log(checkAge(16)); // الناتج: Too young!
console.log(checkAge(21)); // الناتج: Access granted.
```

---

🧪 **5. جرب بنفسك**
```javascript
function double(num) {
  return num * 2;
}

let result = double(5);
console.log("Result:", result); // الناتج: Result: 10
```
حاول تغيير الرقم إلى 10، 15، إلخ.

---

🧠 **النقاط الرئيسية**
*	استخدم `return` لإرسال قيمة مرة أخرى إلى أي مكان تم فيه استدعاء الدالة.
*	`console.log()` تطبع فقط — ولا تُرجع أي شيء.
*	يمكنك حفظ القيم المُرجعة في متغيرات.
*	`return` تُنهي الدالة فورًا.

---

🧪 **تحدي تدريبي**
1.	اكتب دالة باسم `multiply` تأخذ رقمين.
2.	أرجع نتيجة ضربهما.
3.	احفظ النتيجة في متغير واطبعها.

تلميح:
```javascript
function multiply(x, y) {
  return x * y;
}

let output = multiply(6, 7);
console.log(output); // الناتج: 42
```
---