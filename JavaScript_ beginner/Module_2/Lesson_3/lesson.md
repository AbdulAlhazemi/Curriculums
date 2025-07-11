# الوحدة 2: التحكم في التدفق

## الدرس 3: المعامل الثلاثي (Ternary Operator)



🧠 **ماذا ستتعلم**
*	ما هو المعامل الثلاثي
*	كيفية كتابة تعبيرات شرطية سريعة
*	متى تستخدم المعامل الثلاثي بدلاً من `if/else`
*	التعبيرات الثلاثية المتداخلة (مع الحذر)

---

❓ **1. ما هو المعامل الثلاثي؟**

المعامل الثلاثي هو طريقة مختصرة لكتابة جملة `if/else`. إنه رائع للقرارات القصيرة والبسيطة.

البنية (Syntax):
```javascript
condition ? valueIfTrue : valueIfFalse;
```

---

✅ **2. مثال أساسي**
```javascript
let age = 18;
let canVote = age >= 18 ? "Yes" : "No";
console.log(canVote); // الناتج: "Yes"
```

الشرح:
*	إذا كان `age >= 18` صحيحًا (`true`)، يتم إرجاع `"Yes"`
*	وإلا، يتم إرجاع `"No"`

هذا مطابق لـ:
```javascript
if (age >= 18) {
  canVote = "Yes";
} else {
  canVote = "No";
}
```

---

🎯 **3. الاستخدام في المخرجات**

يمكنك استخدامه مباشرة داخل جمل `()console.log` أو `return`:
```javascript
let isLoggedIn = true;

console.log(isLoggedIn ? "Welcome back!" : "Please log in.");
```

---

⚠️ **4. تجنب تعقيده بشكل مفرط**

المعاملات الثلاثية ليست مخصصة للمنطق المعقد. تجنب ربط العديد من المعاملات الثلاثية معًا—فهذا يجعل قراءتها صعبة.

🚫 **سيء:**
```javascript
let score = 90;
let grade = score >= 90 ? "A" : score >= 80 ? "B" : score >= 70 ? "C" : "F";
```

✅ **أفضل (استخدم `if/else` بدلاً من ذلك):**
```javascript
let grade;
if (score >= 90) {
  grade = "A";
} else if (score >= 80) {
  grade = "B";
} else if (score >= 70) {
  grade = "C";
} else {
  grade = "F";
}
```

---

🧪 **جرب بنفسك**

انسخ هذا وشغله في المحرر الخاص بك:
```javascript
let temperature = 30;
let message = temperature > 25 ? "It’s hot!" : "It’s cool!";
console.log(message);
```
حاول تغيير قيمة `temperature` لرؤية مخرجات مختلفة.

---

📌 **حالات الاستخدام الشائعة**
*	عرض إحدى رسالتين
*	إسناد قيمة بناءً على تحقق سريع
*	قرارات بسيطة مدمجة في السطر

---

🧠 **النقاط الرئيسية**
*	المعامل الثلاثي هو اختصار لـ `if/else`
*	استخدمه للشروط البسيطة والقصيرة
*	تجنب استخدام المعامل الثلاثي للقرارات المعقدة والمتداخلة

---