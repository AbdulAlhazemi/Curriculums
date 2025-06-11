## 🟩 الوحدة 1: جافاسكريبت الحديثة والمتقدمة (Advanced JS Foundations)

### 📘 الدرس 2: المفاهيم المتقدمة في الدوال (Closures, Currying, و this)

#### 🧠 **ماذا ستتعلم؟**
* ما هو الإغلاق (Closure) ولماذا هو مهم في جافاسكريPET.
* كيفية استخدام Currying لتصميم دوال مرنة.
* فهم سلوك `this` في جافاسكريبت، خاصة في بيئة الباكند.

---

### 1. ما هو الإغلاق (Closure)؟
الإغلاق هو عندما تحتفظ الدالة بالوصول إلى متغيرات من نطاقها الخارجي حتى بعد انتهاء هذا النطاق.

> 🔍 **مثال:**
> ```javascript
> function outer() {
>   let count = 0;
>   return function inner() {
>     count++;
>     return count;
>   };
> }
> 
> const counter = outer();
> console.log(counter()); // 1
> console.log(counter()); // 2
> ```
> ✅ الدالة `inner` تتذكر المتغير `count` حتى بعد انتهاء تنفيذ `outer`.

> 📌 **لماذا مهم؟**
> * يسمح لك بإنشاء حالات (state) داخل دوال.
> * يُستخدم كثيرًا في الباكند داخل `middleware` أو `factory functions`.

---

### 2. Currying في جافاسكريبت
**Currying** هو تحويل دالة تأخذ أكثر من معطى إلى سلسلة من الدوال، كل واحدة تأخذ معطى واحدًا.

> 🔍 **مثال:**
> ```javascript
> function multiply(a) {
>   return function(b) {
>     return a * b;
>   };
> }
> 
> const double = multiply(2);
> console.log(double(5)); // 10
> ```
> ✳️ **مفيد في:**
> * إعادة استخدام الوظائف.
> * بناء واجهات وظيفية مرنة.
> * تخصيص الدوال حسب السياق.

---

### 3. الكلمة المفتاحية `this` في جافاسكريبت
الكلمة `this` تشير إلى الكائن الذي “يستدعي” الدالة.

⚠️ **تعتمد على السياق:**

🟢 **في كائن:**
```javascript
const user = {
  name: "Yousef",
  greet() {
    return `Hello, ${this.name}`;
  },
};

console.log(user.greet()); // Hello, Yousef
```

🔴 **في دالة مستقلة (strict mode):**
```javascript
function showThis() {
  console.log(this);
}
showThis(); // undefined (في strict mode)
```

🔵 **في دالة سهمية:**
```javascript
const obj = {
  value: 10,
  arrow: () => {
    console.log(this.value); // this هنا لا يشير إلى obj
  },
};

obj.arrow(); // undefined
```
> 📌 **ملخص:**
> * `this` في **الدوال السهمية** = السياق الخارجي.
> * `this` في **الدوال العادية** = الكائن الذي استدعاها.

---


