## 🟦 الوحدة 2: البرمجة غير المتزامنة في جافاسكريبت (Asynchronous JavaScript)

### 📘 الدرس 1: فهم Callbacks وPromises و Async/Await

#### 🧠 **ماذا ستتعلم؟**
* ما هي البرمجة غير المتزامنة ولماذا نحتاجها.
* كيفية التعامل مع العمليات غير المتزامنة باستخدام callbacks.
* كيفية تحسين الكود باستخدام promises.
* استخدام async/await لكتابة كود غير متزامن بشكل أكثر وضوحًا.

---

### 1. لماذا البرمجة غير المتزامنة؟
في جافاسكريبت، يتم تنفيذ الكود **في خيط واحد فقط (single-threaded)**. لذلك، عند التعامل مع عمليات تستغرق وقتًا (مثل القراءة من ملف أو جلب بيانات من API)، لا نريد أن يتوقف البرنامج بالكامل حتى تنتهي.

> 🔔 **الحل؟**
> نستخدم البرمجة غير المتزامنة!

---

### 2. ما هو الـ Callback؟
**Callback** هو دالة تُمرّر كوسيط إلى دالة أخرى وتُنفَّذ لاحقًا.

> 🔍 **مثال:**
> ```javascript
> function greet(name, callback) {
>   console.log("مرحبا " + name);
>   callback();
> }
> 
> greet("أحمد", function() {
>   console.log("تم الترحيب!");
> });
> ```
> ⚠️ **عيب كبير:** إذا تكررت الدوال داخل بعضها، يحصل ما يُعرف بـ **Callback Hell**.

---

### 3. Promises (الوعود)
**Promise** هو كائن يمثل نتيجة عملية غير متزامنة:
* إما `fulfilled` (نجاح)
* أو `rejected` (فشل)

> 🔍 **مثال:**
> ```javascript
> const promise = new Promise((resolve, reject) => {
>   setTimeout(() => resolve("تم!"), 1000);
> });
> 
> promise.then(result => {
>   console.log(result); // "تم!"
> });
> ```
> 🧯 يمكنك استخدام `.catch()` للتعامل مع الأخطاء.

---

### 4. Async / Await
**async/await** تجعل الكود غير المتزامن يبدو وكأنه متزامن.

> 🔍 **مثال:**
> ```javascript
> function wait(ms) {
>   return new Promise(resolve => setTimeout(resolve, ms));
> }
> 
> async function run() {
>   console.log("قبل الانتظار...");
>   await wait(1000);
>   console.log("بعد الانتظار!");
> }
> 
> run();
> ```
> ✅ **مزايا:**
> * كود نظيف.
> * أسهل في القراءة من `.then()` المتكررة.

---

