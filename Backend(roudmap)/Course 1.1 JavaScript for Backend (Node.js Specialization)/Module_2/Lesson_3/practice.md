### 🛠️ تمرين عملي (Practice)
🧩 **المطلوب:**
1.  أنشئ كائن `calculator` يحتوي على دالة `add()` تطبع مجموع رقمين من خصائص الكائن.
2.  جرّب نقل الدالة إلى متغير مستقل ونفذها.
3.  استخدم `bind()` لضمان بقاء `this` يشير للكائن.

✍️ **نموذج البدء:**
```javascript
const calculator = {
  a: 5,
  b: 10,
  add() {
    console.log(this.a + this.b);
  }
};

const sum = calculator.add;
// sum(); // لن تعمل كما هو متوقع

const boundSum = sum.bind(calculator);
boundSum(); // 15
```
> 💡 **تلميح:** عندما تنقل دالة من كائن إلى مكان آخر، تفقد `this` مرجعها.

***