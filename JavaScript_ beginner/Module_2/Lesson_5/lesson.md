# الوحدة 2: التحكم في التدفق

## الدرس 5: حلقات `for`

🧠 **ماذا ستتعلم**
*	كيفية استخدام حلقات `for` للعد والتكرار
*	الأجزاء الرئيسية الثلاثة لحلقة `for`
*	متى تستخدم `for` مقابل `while`
*	المرور على المصفوفات (مقدمة موجزة)

---

🔁 **1. ما هي حلقة `for`؟**

حلقة `for` هي طريقة شائعة لتكرار الكود لعدد معين من المرات. إنها مدمجة وقوية.

البنية (Syntax):
```javascript
for (initialization; condition; update) {
  // الكود المراد تنفيذه
}
```

---

👀 **2. تفصيل الأجزاء**

لنلقِ نظرة على مثال:
```javascript
for (let i = 1; i <= 5; i++) {
  console.log("i is", i);
}
```

هذه الحلقة لها 3 أجزاء:
*	**التهيئة (Initialization):** `let i = 1` ← ابدأ العد من 1
*	**الشرط (Condition):** `i <= 5` ← استمر طالما أن `i` أصغر من أو يساوي 5
*	**التحديث (Update):** `i++` ← أضف 1 إلى `i` بعد كل دورة

الناتج:
```
i is 1
i is 2
i is 3
i is 4
i is 5
```

---

🔄 **3. التكرار العكسي**

يمكنك العد تنازليًا أيضًا!
```javascript
for (let i = 5; i > 0; i--) {
  console.log(i);
}
```

---

🧠 **4. لماذا نستخدم `for` بدلاً من `while`؟**

استخدم `for` عندما:
*	تعرف عدد المرات التي يجب أن تعمل فيها الحلقة
*	تقوم بالعد (مثلًا من 1 إلى 10)

استخدم `while` عندما:
*	لا تعرف عدد المرات التي تحتاج فيها إلى التكرار
*	تنتظر تغيير شرط ما (مثل إدخال المستخدم)

---

🧪 **5. جرب بنفسك**
```javascript
for (let i = 0; i < 3; i++) {
  console.log("Hello, world!");
}
```
كم مرة يتم طباعتها؟ حاول تغيير الشرط!

---

⚠️ **6. خطر الحلقة اللانهائية**

تمامًا مثل `while`، يمكنك إنشاء حلقة لا نهائية إذا نسيت التحديث:
```javascript
for (let i = 0; i < 5;) {// هذا سيجمد متصفحك!
  console.log(i); 
}
```
 القيمة لا تتغير أبدًا

✅ تأكد دائمًا من تضمين تحديث مناسب في حلقتك.

---

📚 **7. معاينة مصغرة: المرور عبر المصفوفات**

ستتعلم المزيد عن المصفوفات قريبًا، ولكن إليك نظرة سريعة:
```javascript
let fruits = ["apple", "banana", "cherry"];

for (let i = 0; i < fruits.length; i++) {
  console.log(fruits[i]);
}
```
هذه الحلقة تمر على كل عنصر في المصفوفة!

---

🧠 **النقاط الرئيسية**
*	حلقات `for` هي الأفضل للتكرار المعروف ذي الطول الثابت
*	تشمل البدء، والتوقف، والخطوة — كلها في مكان واحد
*	راقب دائمًا شروط الحلقة لتجنب الحلقات اللانهائية


---