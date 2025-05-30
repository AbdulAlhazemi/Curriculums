# الوحدة 3: الدوال (Functions)

## الدرس 4: نطاق الدالة (Function Scope)

🧠 **ماذا ستتعلم**
*	ماذا يعني النطاق (scope) في جافاسكريبت
*	الفرق بين النطاق العام (global) والنطاق المحلي (local)
*	كيف تنشئ الدوال نطاقها الخاص
*	لماذا يساعد النطاق في منع التعارض بين المتغيرات

---

🌐 **1. ما هو النطاق (Scope)؟**

يشير النطاق إلى المكان الذي يمكن فيه الوصول إلى المتغير في الكود الخاص بك.

هناك نوعان رئيسيان:
*	**النطاق العام (Global Scope)** – المتغيرات المُعلنة خارج الدوال
*	**النطاق المحلي (Local Scope)** – المتغيرات المُعلنة داخل الدوال

---

🏠 **2. النطاق العام (Global Scope)**

يمكن الوصول إلى المتغيرات المُعلنة خارج أي دالة من أي مكان في الكود الخاص بك.
```javascript
let name = "Chris";

function greet() {
  console.log("Hello, " + name);
}

greet(); // الناتج: Hello, Chris
```
المتغير `name` متاح داخل الدالة `greet()` لأنه عام (global).

---

🛠️ **3. النطاق المحلي (Function Scope)**

المتغيرات المُعلنة داخل الدالة يمكن استخدامها فقط داخل تلك الدالة.
```javascript
function showAge() {
  let age = 25;
  console.log("Age:", age);
}

showAge();      // الناتج: Age: 25
console.log(age); // ❌ خطأ: age غير معرّف
```
المتغير `age` محلي بالنسبة للدالة `showAge` ولا وجود له خارجها.

---

🔄 **4. إعادة استخدام أسماء المتغيرات في نطاقات مختلفة**

يمكن للمتغيرات في نطاقات مختلفة استخدام نفس الاسم دون تعارض.
```javascript
let message = "Hello from global";

function test() {
  let message = "Hello from local";
  console.log(message); // النسخة المحلية
}

test();               // الناتج: Hello from local
console.log(message); // الناتج: Hello from global
```
المتغيرات المحلية "تحجب" (shadow) المتغيرات العامة داخل الدالة.

---

📏 **5. لماذا النطاق مهم؟**

النطاق:
*	يساعد على تجنب تعارض المتغيرات العرضي
*	يحافظ على الكود الخاص بك معياريًا ونظيفًا
*	يجعل تصحيح الأخطاء أسهل

---

🧪 **جرب بنفسك**
```javascript
let animal = "Dog";

function speak() {
  let animal = "Cat";
  console.log("Inside:", animal);
}

speak();               // الناتج: Inside: Cat
console.log("Outside:", animal); // الناتج: Outside: Dog
```

---

🧠 **النقاط الرئيسية**
*	المتغيرات العامة يمكن الوصول إليها من أي مكان
*	المتغيرات المحلية توجد فقط داخل دوالها
*	الدوال تنشئ نطاقًا جديدًا في كل مرة يتم تشغيلها
*	المتغيرات في النطاق المحلي تتجاوز (override) المتغيرات العامة داخل الدالة

---

🧪 **تحدي تدريبي**
1.	قم بالإعلان عن متغير عام `user = "Alice"`
2.	أنشئ دالة `changeUser()` تحتوي على متغير محلي يسمى أيضًا `user = "Bob"`
3.	داخل الدالة، اطبع `user`
4.	خارج الدالة، اطبع المتغير `user` العام

تلميح:
```javascript
let user = "Alice";

function changeUser() {
  let user = "Bob";
  console.log("Inside:", user); // الناتج: Bob
}

changeUser();
console.log("Outside:", user); // الناتج: Alice
```
---