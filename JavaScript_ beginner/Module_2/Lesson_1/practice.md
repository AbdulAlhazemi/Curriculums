## 🧪 تحدي تدريبي: استخدام جمل if / else if / else

### 🎯 التحدي:

في محرر JavaScript الخاص بك:

1. أعلن عن متغير باسم `hour`، واضبط قيمته على رقم بين **0 و 23**.  
2. اكتب سلسلة شرطية باستخدام `if / else if / else` كالتالي:
   - إذا كانت `hour` أقل من 12 → اطبع `"Good morning!"`  
   - إذا كانت `hour` أقل من 18 → اطبع `"Good afternoon!"`  
   - خلاف ذلك → اطبع `"Good evening!"`  
3. جرب تغيير قيمة `hour` إلى أوقات مختلفة (مثل: 9، 15، 20) ولاحظ النتيجة في وحدة التحكم.

---

### 💡 تلميحات:

- تأكد من استخدام القيم الرقمية (مثال: `;let hour = 10`)
- استخدم `()console.log` لطباعة الرسائل.
- ترتيب الشروط مهم! (ابدأ من الأصغر فالأكبر)

---

### ✅ الحل النموذجي:

```javascript
let hour = 10;

if (hour < 12) {
  console.log("Good morning!");
} else if (hour < 18) {
  console.log("Good afternoon!");
} else {
  console.log("Good evening!");
}

// جرّب تغيير قيمة hour مثل:
// hour = 15;
// hour = 20;
```