## 🟩 الوحدة 4: التعامل مع الأخطاء وتصحيحها (Error Handling & Debugging)

### 📘 الدرس 1: استراتيجيات التعامل مع الأخطاء في Node.js

#### 🧠 **ماذا ستتعلم؟**
* الفرق بين الأخطاء المتزامنة وغير المتزامنة.
* كيفية استخدام `try/catch` في جافاسكريبت وNode.js.
* نمط الأخطاء في الاستدعاءات الراجعة (Callback-style error-first).
* التعامل مع الأخطاء في الوعود (Promises).
* إنشاء معالجات أخطاء عامة في تطبيقات Node.js.

***

### 1. أنواع الأخطاء في Node.js

🔸 **أخطاء متزامنة (Synchronous Errors):**
تحدث داخل كتلة كود يمكن التعامل معها مباشرة باستخدام `try/catch`.

🔸 **أخطاء غير متزامنة (Asynchronous Errors):**
تحدث لاحقًا بعد تنفيذ الكود الأساسي، مثل داخل `callbacks` أو `promises`.

***

### 2. استخدام `try/catch`
```javascript
try {
  let data = JSON.parse("invalid json"); // This will throw an error
  console.log(data);
} catch (error) {
  console.error("حدث خطأ:", error.message);
}
```
> 📌 تعمل فقط مع الكود المتزامن. لا يمكنك استخدامها لاحتواء خطأ من دالة غير متزامنة مثل `setTimeout`.

***

### 3. نمط Callback-style error-first
في Node.js، كثير من الدوال غير المتزامنة تستخدم نمط الخطأ كأول وسيط في دالة الـ callback.

```javascript
const fs = require('fs');

fs.readFile('non_existent_file.txt', 'utf8', (err, data) => {
  if (err) {
    console.error("خطأ في قراءة الملف:", err);
    return; // Important to stop execution
  }
  console.log("محتوى الملف:", data);
});
```

***

### 4. التعامل مع Promises
تستخدم سلسلة `.catch()` للتعامل مع أي خطأ يحدث في الـ Promise.

```javascript
fetch('https://invalid.url/data') // Assuming fetch is available (e.g., with node-fetch)
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error("خطأ:", error));
```

***

### 5. Async/Await + `try/catch`
هذه هي الطريقة الحديثة والأنظف للتعامل مع أخطاء الكود غير المتزامن.

```javascript
async function getData() {
  try {
    let response = await fetch('https://invalid.url/data');
    let data = await response.json();
    console.log(data);
  } catch (error) {
    console.error("حدث خطأ:", error);
  }
}
getData();
```

***

### 6. معالجات الأخطاء العامة
يمكنك التقاط الأخطاء غير المتوقعة على مستوى التطبيق لمنع توقف البرنامج بشكل مفاجئ.

```javascript
// To catch synchronous errors that were not handled
process.on('uncaughtException', (err) => {
  console.error('خطأ غير متوقع لم يتم التعامل معه:', err);
  process.exit(1); // It's often recommended to exit after an uncaught exception
});

// To catch promise rejections that were not handled
process.on('unhandledRejection', (reason, promise) => {
  console.error('وعد مرفوض لم يتم التعامل معه:', reason);
});
```

***

