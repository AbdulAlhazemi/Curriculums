# الوحدة 4: المصفوفات والكائنات

## الدرس 5: دوال الكائن (Object Methods)



🧠 **ماذا ستتعلم**
*	ما هي الدوال (methods) الموجودة داخل الكائنات
*	كيفية تعريف واستدعاء الدوال (methods)
*	كيفية استخدام الكلمة المفتاحية `this` للإشارة إلى الكائن نفسه

---

🛠️ **1. ما هي دالة الكائن (Object Method)؟**

الدالة (method) هي وظيفة (function) مخزنة داخل كائن.
```javascript
let person = {
  name: "Ella",
  greet: function () {
    console.log("Hello!");
  }
};
```

يمكنك استدعاؤها هكذا:
```javascript
person.greet(); // الناتج: "Hello!"
```

---

✅ **2. صياغة مختصرة للدوال (Shorthand Method Syntax)**

هناك طريقة أقصر لتعريف الدوال داخل الكائنات:
```javascript
let dog = {
  name: "Buddy",
  bark() {
    console.log("Woof!");
  }
};

dog.bark(); // الناتج: "Woof!"
```

---

🔁 **3. استخدام `this` في الدوال**

داخل الدالة (method)، تشير `this` إلى الكائن الذي تنتمي إليه الدالة.
```javascript
let user = {
  username: "coder123",
  sayHello() {
    console.log("Hi, I'm " + this.username);
  }
};

user.sayHello(); // الناتج: "Hi, I'm coder123"
```
⚠️ `this.username` تصل إلى خاصية `username` للكائن.

---

🧪 **جرب بنفسك**
```javascript
let car = {
  brand: "Tesla",
  model: "Model S",
  displayInfo() {
    console.log("Car: " + this.brand + " " + this.model);
  }
};

car.displayInfo(); // الناتج: "Car: Tesla Model S"
```

---

❗ **4. دوال الكائن مقابل الدوال العادية**

إذا قمت بتعريف دالة خارج الكائن، فلن تحتوي على `this` تشير إلى ذلك الكائن.
```javascript
function sayHi() {
  console.log("Hi!");
}

sayHi(); // تعمل، ولكنها غير مرتبطة بأي كائن
```

---

🧠 **النقاط الرئيسية**
*	دوال الكائن هي وظائف (functions) مخزنة داخل الكائنات.
*	استخدم الصياغة المختصرة ` {}()methodName`.
*	استخدم `this` للإشارة إلى خصائص أخرى داخل نفس الكائن.
*	استدعِ الدوال باستخدام `()object.methodName`.


---