## 📝 اختبار الدرس 4: سلسلة النطاقات والبيئة المعجمية

اختر الإجابة الصحيحة لكل سؤال:

### السؤال 1:
ما هو النطاق (Scope) في JavaScript؟

A. نوع من أنواع الأحداث
B. طريقة لتغيير الألوان
C. **المكان الذي يمكن فيه الوصول إلى المتغيرات**
D. مكتبة خارجية

✅ **الإجابة الصحيحة:** C

---

### السؤال 2:
ما الذي يحدد البيئة المعجمية (Lexical Environment) للمتغيرات؟

A. **مكان كتابة المتغير في الكود**
B. نوع المتغير (`var`, `let`, `const`) فقط
C. المتصفح المستخدم
D. ترتيب الاستدعاء

✅ **الإجابة الصحيحة:** A

---

### السؤال 3:
أي من التعريفات التالية يُعتبر **تظليلًا (Shadowing)**؟
```javascript
let x = 10;

function example() {
  let x = 5;
  console.log(x);
}
```
A. لا يوجد تظليل هنا
B. **نعم، `x` في الدالة تظلل `x` العالمية**
C. `x` غير معرف داخل الدالة
D. سيطبع 10 دائمًا

✅ **الإجابة الصحيحة:** B

---

### السؤال 4:
ماذا يحدث إذا لم تجد JavaScript متغيرًا في النطاق الحالي؟

A. تقوم بتعطيل الكود
B. تعود إلى DOM تلقائيًا
C. **تبحث في النطاق الأعلى (Scope Chain)**
D. تحذفه من الذاكرة

✅ **الإجابة الصحيحة:** C

---

### السؤال 5:
ما نوع النطاق الناتج عن استخدام `let` داخل `{}`؟

A. نطاق عالمي
B. نطاق دالة
C. **نطاق كتلة (Block Scope)**
D. ليس له نطاق

✅ **الإجابة الصحيحة:** C

---

هل ترغب أن أُكمل بـ **الدرس 5: محرك JavaScript (The JavaScript Engine)** الآن؟