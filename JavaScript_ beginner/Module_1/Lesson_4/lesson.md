# الوحدة 1: أساسيات جافاسكريبت

## الدرس 4 : أنواع البيانات الأولية



🧠 **ماذا ستتعلم**
*	ما هي أنواع البيانات الأولية
*	كيفية استخدام السلاسل النصية (string)، الأرقام (number)، القيم المنطقية (boolean)، `null`، و `undefined`
*	كيفية التحقق من أنواع البيانات باستخدام `typeof`
*	حالات الاستخدام الشائعة وأمثلة لكل نوع

---

📦 **1. ما هي أنواع البيانات الأولية؟**

في جافاسكريبت، أنواع البيانات الأولية هي اللبنات الأساسية للبيانات.
يوجد 7 أنواع إجمالاً، ولكن في هذا الدرس، سنركز على الـ 5 الأكثر شيوعًا:
1.	السلسلة النصية (string)
2.	الرقم (number)
3.	القيمة المنطقية (boolean)
4.	`null`
5.	`undefined`

كل نوع يمثل نوعًا مختلفًا من البيانات التي يمكن لمتغيراتك تخزينها.

---

🔤 **2. السلسلة النصية (String)**

السلسلة النصية هي أي نص داخل علامتي اقتباس (' ' أو " ").
```javascript
let name = "Amira";
let greeting = 'Hello!';
```

يمكنك دمج السلاسل النصية باستخدام المعامل `+`:
```javascript
let fullName = "Amira" + " " + "Khan";
console.log(fullName); // الناتج: Amira Khan
```

---

🔢 **3. الرقم (Number)**

الرقم هو أي قيمة عددية — سواء كانت أعدادًا صحيحة أو عشرية.
```javascript
let age = 30;
let temperature = 36.6;
```

يمكنك إجراء عمليات حسابية باستخدام الأرقام:
```javascript
let total = 5 + 3;
console.log(total); // الناتج: 8
```

---

✅ **4. القيمة المنطقية (Boolean)**

القيمة المنطقية لها قيمتان فقط: `true` أو `false`.
تُستخدم للمنطق واتخاذ القرارات.
```javascript
let isLoggedIn = true;
let hasPermission = false;
```

---

🚫 **5. Null**

تُستخدم `null` عندما يُراد لمتغير ألا يحمل أي قيمة عن قصد.
```javascript
let middleName = null;
```

إنها كأنك تقول: "هذا فارغ حاليًا."

---

❓ **6. Undefined**

تعني `undefined` أن المتغير قد تم الإعلان عنه ولكن لم تُسند إليه قيمة بعد.
```javascript
let score;
console.log(score); // الناتج: undefined
```

تمنح جافاسكريبت القيمة `undefined` تلقائيًا إذا نسيت إسناد قيمة.

---

🧪 **جرب بنفسك**

في المحرر الخاص بك، جرب الإعلان عن متغير واحد من كل نوع:
```javascript
let name = "Rami";      // سلسلة نصية (string)
let age = 20;           // رقم (number)
let isStudent = true;   // قيمة منطقية (boolean)
let nickname = null;    // null
let lastLogin;          // undefined

console.log(name, age, isStudent, nickname, lastLogin);
```

---

🧪 **7. التحقق من النوع باستخدام `typeof`**

يوجد في جافاسكريبت معامل مدمج يسمى `typeof` يخبرك بنوع المتغير:
```javascript
let value = 42;
console.log(typeof value); // الناتج: "number"
```

جرب هذا مع أنواع مختلفة:
```javascript
console.log(typeof "Hello");      // الناتج: "string"
console.log(typeof true);         // الناتج: "boolean"
console.log(typeof null);         // الناتج: "object" ← (أمر غريب في جافاسكريبت!)
console.log(typeof undefined);  // الناتج: "undefined"
```

---

💡 **أمر غريب في جافاسكريبت: `typeof null`**

نتيجة `typeof null` هي `"object"` — هذا خطأ معروف في جافاسكريبت ولن يتم إصلاحه لأسباب تتعلق بالتوافق مع الإصدارات القديمة.

فقط تذكر: `null` تعني فراغًا مقصودًا، حتى لو أظهر `typeof` القيمة `"object"`.

---

🧠 **النقاط الرئيسية**
*	استخدم السلاسل النصية للنصوص، والأرقام للعمليات الحسابية، والقيم المنطقية للمنطق.
*	استخدم `null` لتعني "لا قيمة عن قصد".
*	استخدم `undefined` لتمثيل "لم يتم التعيين بعد".
*	استخدم `typeof` للتحقق من نوع القيمة.

---