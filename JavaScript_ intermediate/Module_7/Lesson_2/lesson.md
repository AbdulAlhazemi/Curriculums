Of course, here is Lesson 2 on Currying, formatted in Markdown.

# الوحدة 7: أنماط كتابة الكود المتقدمة
**(Advanced Code Patterns)**

## الدرس 2: الكارينج (Currying)

🧠 **ماذا ستتعلم**
* ما هو الكارينج (Currying) في البرمجة.
* كيف نحول دالة تأخذ عدة معاملات إلى سلسلة من الدوال التي تأخذ معاملًا واحدًا.
* فوائد الكارينج في تحسين قابلية إعادة الاستخدام وكتابة كود نظيف.
* تطبيق عملي على الكارينج في JavaScript.

---

### 🧾 1. ما هو الكارينج؟

**الكارينج (Currying)** هو أسلوب لتحويل دالة تأخذ عدة معاملات (Arguments) إلى دالة تأخذ معاملًا واحدًا فقط، ثم تُعيد دالة تأخذ المعامل التالي، وهكذا، حتى يتم استلام كل المعاملات.

بمعنى آخر، الكارينج يحول دالة من الشكل:
`f(a, b, c)`

إلى سلسلة دوال مثل:
`f(a)(b)(c)`

---

### 🧠 مثال عملي:
```javascript
function multiply(a) {
  return function(b) {
    return a * b;
  };
}

const multiplyBy2 = multiply(2);

console.log(multiplyBy2(5)); // 10
console.log(multiplyBy2(10)); // 20
```
في المثال السابق، `multiply(2)` تُعيد دالة تأخذ `b` وتضربه في 2.

---

### 📚 2. لماذا نستخدم الكارينج؟
* لتجزئة الدوال الكبيرة إلى وظائف أصغر وقابلة لإعادة الاستخدام.
* لتثبيت بعض المعاملات مسبقًا (Partial Application).
* لتحسين قابلية التركيب (Composition) في البرمجة الوظيفية.

---

### 🔧 3. مثال على الدالة الكاملة:
```javascript
function add(a) {
  return function(b) {
    return function(c) {
      return a + b + c;
    };
  };
}

console.log(add(1)(2)(3)); // 6
```
---

### ⚙️ 4. تحويل دالة عادية إلى دالة كارينج تلقائيًا
```javascript
function curry(fn) {
  return function curried(...args) {
    if (args.length >= fn.length) {
      return fn.apply(this, args);
    } else {
      return function(...nextArgs) {
        return curried.apply(this, args.concat(nextArgs));
      };
    }
  };
}

// مثال:
function sum(a, b, c) {
  return a + b + c;
}

const curriedSum = curry(sum);

console.log(curriedSum(1)(2)(3)); // 6
console.log(curriedSum(1, 2)(3)); // 6
```
---

### 🚀 ماذا بعد؟
في الدرس القادم، سنتناول موضوع **جحيم الاستدعاءات (Callback Hell)** وكيف يمكننا تحسين كتابة الكود غير المتزامن باستخدام Promises و Async/Await.

---
---

