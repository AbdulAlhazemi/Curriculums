# الوحدة 2: الأحداث والتفاعلية

## الدرس 3: دالة `()addEventListener`


🧠 **ماذا ستتعلم**
*	كيفية استخدام `()addEventListener` للاستجابة للأحداث
*	بنية وتركيب `()addEventListener`
*	إرفاق عدة مستمعات (listeners) بنفس العنصر
*	إزالة مستمعات الأحداث عند الحاجة

---

🔍 **1. ما هي `()addEventListener`؟**

تتيح لك دالة `()addEventListener` الاستماع إلى الأحداث على عنصر وتشغيل دالة رد نداء (callback function) عند وقوع ذلك الحدث.

هذه هي الطريقة الأكثر مرونة وحداثة للتعامل مع الأحداث في جافاسكريبت.

---

🛠️ **2. البنية الأساسية**

```javascript
element.addEventListener(eventType, callbackFunction);
```
*	`eventType`: سلسلة نصية مثل `"click"`، `"input"`، `"submit"`، إلخ.
*	`callbackFunction`: الدالة التي سيتم تشغيلها عند إطلاق الحدث.

مثال:
```javascript
const btn = document.querySelector("#greet");

btn.addEventListener("click", () => {
  console.log("Hello, user!");
});
```

---

💡 **3. الدالة المسماة مقابل الدالة المجهولة (Anonymous Function)**

كلاهما يعمل، ولكن يمكن إعادة استخدام الدوال المسماة أو إزالتها لاحقًا.

**دالة مجهولة:**
```javascript
btn.addEventListener("click", () => {
  alert("Clicked!");
});
```

**دالة مسماة:**
```javascript
function greetUser() {
  alert("Welcome!");
}

btn.addEventListener("click", greetUser);
```

---

🔁 **4. إضافة عدة مستمعات**

يمكنك إرفاق عدة مستمعات أحداث بنفس العنصر، حتى لنفس نوع الحدث:
```javascript
btn.addEventListener("click", greetUser);
btn.addEventListener("click", () => {
  console.log("This runs too!");
});
```
يتم تشغيل كل واحدة بالترتيب الذي تمت إضافتها به.

---

🔄 **5. إزالة مستمع حدث**

لإزالة مستمع، يجب عليك استخدام دالة مسماة واستدعاء `removeEventListener()`:
```javascript
function handleClick() {
  console.log("Button clicked!");
}

btn.addEventListener("click", handleClick);

// لاحقًا في الكود
btn.removeEventListener("click", handleClick);
```
لا يمكن إزالة الدوال المجهولة لأنه لا يوجد مرجع إليها.

---

🧠 **النقاط الرئيسية**
*	`addEventListener()` هي أفضل طريقة للاستجابة لتفاعلات المستخدم.
*	استخدم الدوال المسماة إذا كنت تخطط لإزالتها لاحقًا.
*	يمكنك إرفاق عدة مستمعات بعنصر واحد.

---