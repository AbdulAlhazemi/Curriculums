## 🟦 الوحدة 2: البرمجة غير المتزامنة في جافاسكريبت (Asynchronous JavaScript)

### 📘 الدرس 3: فهم `this` والسياق (Context) في جافاسكريبت

#### 🧠 **ماذا ستتعلم؟**
* معنى الكلمة المفتاحية `this` في جافاسكريبت.
* الفرق بين السياق (context) في الدوال العادية والـ arrow functions.
* كيف يختلف `this` في الكائنات، الدوال، والأحداث.
* كيف يؤثر الاستدعاء (call, apply, bind) على قيمة `this`.

***

### 1. ما هو `this`؟
الكلمة المفتاحية `this` تشير إلى **الكائن الذي “يمتلك” السياق الحالي للتنفيذ**. تختلف قيمتها حسب طريقة استدعاء الدالة.

### 2. `this` في السياق العام (Global)
```javascript
console.log(this); // في المتصفح: يشير إلى window
```
> في Node.js، `this` في السياق العام لا تشير إلى `global` وإنما إلى كائن فارغ `{}`.

### 3. `this` داخل كائن (Object)
```javascript
const user = {
  name: "Ali",
  greet() {
    console.log(`مرحبًا، أنا ${this.name}`);
  }
};

user.greet(); // this => user
```
> ✅ لأن الدالة تم استدعاؤها من داخل الكائن.

### 4. `this` داخل دالة مستقلة
```javascript
function sayHi() {
  console.log(this);
}

sayHi(); // في المتصفح: this => window
```
> ⚠️ في الوضع الصارم `"use strict"`، ستكون `this` غير معرّفة (undefined).

### 5. الفرق بين الدوال العادية و Arrow Functions
```javascript
const person = {
  name: "Sara",
  greet: function () {
    console.log(this.name);
  },
  arrowGreet: () => {
    console.log(this.name);
  }
};

person.greet();       // "Sara"
person.arrowGreet();  // undefined (this لا تشير إلى الكائن)
```
> 📌 **السبب:** الدوال العادية تأخذ `this` من **الكائن المُستدعي**، بينما `arrow function` تأخذ `this` من **السياق المحيط**.

### 6. تغيير `this` باستخدام `bind`, `call`, `apply`
```javascript
function greet() {
  console.log(`Hi, I'm ${this.name}`);
}

const user = { name: "Lina" };

greet.call(user);  // Hi, I'm Lina
greet.apply(user); // Hi, I'm Lina

const bound = greet.bind(user);
bound();           // Hi, I'm Lina
```
| الطريقة | تمرير المعاملات | التأثير على `this` |
| :--- | :--- | :--- |
| **`call()`** | مفصولة بفواصل | ينفذ الدالة فورًا |
| **`apply()`** | كمصفوفة | ينفذ الدالة فورًا |
| **`bind()`** | مفصولة بفواصل | يُعيد دالة جديدة بربط `this` ✅ |

***



### ❓ اختبار (Quiz)
1.  **ما هي قيمة `this` في الدالة التالية داخل المتصفح؟**
    ```javascript
    function test() {
      console.log(this);
    }
    test();
    ```
    * A) الكائن global في Node
    * B) undefined
    * C) window ✅
    * D) null

2.  **ماذا تُعيد `arrow function` عندما تستخدم `this`؟**
    * A) دائمًا `window`
    * B) تأخذ `this` من السياق المحيط ✅
    * C) تشير للكائن الحالي
    * D) undefined دائمًا

3.  **ما الفرق بين `call()` و `bind()`؟**
    * A) لا يوجد فرق
    * B) `call()` يعيد دالة جديدة
    * C) `bind()` يعيد دالة جديدة دون تنفيذها ✅
    * D) `bind()` ينفذ الدالة مباشرة

4.  **في أي حالة تكون قيمة `this` هي `undefined`؟**
    * A) في الكائنات
    * B) داخل الدوال في الوضع الصارم ✅
    * C) دائمًا في `setTimeout`
    * D) في `arrow functions`

5.  **ما ناتج الكود التالي؟**
    ```javascript
    const user = {
      name: "Mona",
      greet: function () {
        console.log(this.name);
      }
    };

    const g = user.greet;
    g(); // ؟
    ```
    * A) “Mona”
    * B) undefined ✅
    * C) خطأ
    * D) null

***