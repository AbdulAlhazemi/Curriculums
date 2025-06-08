# الوحدة 2: التحكم في التدفق

## الدرس 2: جُمل `switch`



🧠 **ماذا ستتعلم**
*	متى وكيف تستخدم جُمل `switch`
*	كيف تعمل `case` و `break`
*	دور `default`
*	متى تختار `switch` بدلاً من `if/else`

---

🔄 **1. ما هي جملة `switch`؟**

جملة `switch` هي بديل لسلاسل `if/else if/else`. تكون مفيدة عندما تتحقق من نفس القيمة مقابل عدة احتمالات.

مثال:
```javascript
let day = "Monday";

switch (day) {
  case "Monday":
    console.log("Start of the week!");
    break;
  case "Friday":
    console.log("Almost the weekend!");
    break;
  default:
    console.log("Just another day.");
}
```

---

🧩 **2. تفصيل البنية (Syntax)**

```javascript
switch (expression) {
  case value1:
    // الكود الذي يُنفذ إذا كانت قيمة `expression` تساوي `value1`
    break;
  case value2:
    // الكود الذي يُنفذ إذا كانت قيمة `expression` تساوي `value2`
    break;
  default:
    // الكود الذي يُنفذ في حال عدم تطابق أي `case`
}
```

---

🛑 **3. لماذا نستخدم `break`؟**

بدون `break`، تستمر جافاسكريبت في تنفيذ الحالات (`case`) التالية، حتى لو تطابقت إحداها بالفعل. هذا يسمى "السقوط" (fall-through).

مثال:
```javascript
let color = "blue";

switch (color) {
  case "red":
    console.log("Red!");
  case "blue":
    console.log("Blue!");
  case "green":
    console.log("Green!");
}
```

الناتج:
```
Blue!
Green!
```

✅ مع `break`:
```javascript
switch (color) {
  case "red":
    console.log("Red!");
    break;
  case "blue":
    console.log("Blue!");
    break;
  case "green":
    console.log("Green!");
    break;
}
```

الناتج:
```
Blue!
```

---

❓ **4. استخدام `default`**

يتم تنفيذ `default` عندما لا تتطابق أي `case`.
```javascript
let fruit = "banana";

switch (fruit) {
  case "apple":
    console.log("It's an apple.");
    break;
  case "orange":
    console.log("It's an orange.");
    break;
  default:
    console.log("Unknown fruit.");
}
```

---

🤔 **5. متى نستخدم `switch` بدلاً من `if/else`؟**

استخدم `switch` عندما:
*	تتحقق من متغير واحد مقابل العديد من القيم المعروفة
*	تريد كودًا أنظف وأكثر قابلية للقراءة

استخدم `if/else` عندما:
*	تقارن بين شروط متعددة
*	الشروط لا تعتمد على نفس المتغير

---

🧪 **جرب بنفسك**

في المحرر الخاص بك:
```javascript
let role = "admin";

switch (role) {
  case "admin":
    console.log("Welcome, Admin!");
    break;
  case "editor":
    console.log("Welcome, Editor!");
    break;
  case "viewer":
    console.log("Welcome, Viewer!");
    break;
  default:
    console.log("Access denied.");
}
```
حاول تغيير قيمة `role` وشغل الكود مرة أخرى!

---

🧠 **النقاط الرئيسية**
*	`switch` تتحقق من قيمة واحدة مقابل عدة حالات (`case`)
*	استخدم `break` لإيقاف "السقوط" (fall-through)
*	استخدم `default` للحالات غير المتطابقة
*	رائع لكود نظيف عند التعامل مع العديد من الخيارات الثابتة

---