# الوحدة 7: أنماط كتابة الكود المتقدمة
**(Advanced Code Patterns)**

## الدرس 1: الإغلاقات (Closures)

🧠 **ماذا ستتعلم**
* ما هو الإغلاق (Closure).
* كيف تحتفظ الدالة بالوصول إلى متغيرات خارجية.
* حالات استخدام عملية للإغلاقات.
* فوائد ومخاطر استخدام الإغلاقات.

---

### 🧾 1. ما هو الإغلاق؟

**الإغلاق (Closure)** هو قدرة دالة في JavaScript على **تذكر والوصول إلى المتغيرات** من **النطاق الذي تم إنشاؤها فيه**، حتى بعد انتهاء هذا النطاق.

📌 الإغلاق يحدث عندما تُعيد دالة داخلية من دالة خارجية، وتستمر في الوصول إلى متغيرات الدالة الأصلية.

---

### 🧠 مثال عملي:

```javascript
function outer() {
  let counter = 0;

  return function inner() {
    counter++;
    console.log(counter);
  };
}

const count = outer();

count(); // 1
count(); // 2
count(); // 3
```
✅ الدالة `inner` حافظت على الوصول إلى المتغير `counter` حتى بعد انتهاء `outer` — وهذا هو الإغلاق.

---

### 📚 2. لماذا نستخدم الإغلاقات؟

* للحفاظ على الحالة دون كشفها للعالم الخارجي.
* لإنشاء **دوال مخصصة (Factories)**.
* لإنشاء **أحداث خاصة** أو **مؤقتات مستقلة**.

---

### 🔐 3. حالة استخدام شائعة: حماية البيانات

```javascript
function createUser(name) {
  let password = "secret123";

  return {
    getName: () => name,
    checkPassword: (input) => input === password
  };
}

const user = createUser("Mona");

console.log(user.getName()); // Mona
console.log(user.checkPassword("wrong")); // false
console.log(user.checkPassword("secret123")); // true
```
✅ تم “تغليف” `password` داخل الإغلاق ولا يمكن الوصول إليه مباشرة.

---

### ⚠️ 4. ملاحظة مهمة:

الإغلاقات يمكن أن تسبب مشاكل إذا احتفظت بالكثير من الذاكرة لفترة طويلة (Memory Leaks)، خصوصًا داخل الأحداث أو المؤقتات.

---

### 👁️‍🗨️ مثال من الواقع

في تطبيقات الويب، يمكن استخدام الإغلاقات لإنشاء أزرار تتذكر عدد النقرات لكل زر على حدة:

```javascript
function createClickCounter() {
  let clicks = 0;
  return function () {
    clicks++;
    console.log(`Clicked ${clicks} times`);
  };
}

const btn1 = createClickCounter();
const btn2 = createClickCounter();

btn1(); // Clicked 1 times
btn2(); // Clicked 1 times
btn1(); // Clicked 2 times
```
---

### 🚀 ماذا بعد؟

في الدرس القادم سنتعرف على **الكارينج (Currying)** — أسلوب لتحويل الدوال إلى سلاسل من الدوال الجزئية.

---