# الوحدة 5: JSON والتعامل مع واجهات برمجة التطبيقات (APIs)

## الدرس 5: صيغة `async/await`


🧠 **ماذا ستتعلم**
*	ماذا تفعل الكلمتان المفتاحيتان `async` و `await`
*	كيف تبسّط `async/await` العمل مع الـ Promises
*	معالجة الأخطاء باستخدام `try/catch` في دوال `async`

---

🔍 **1. ما هي `async/await`؟**

`Async/await` هي "سكر نحوي" (syntactic sugar) مبني فوق الـ Promises لكتابة كود غير متزامن يبدو ويتصرف كأنه كود متزامن.
*	`async` تحدد الدالة على أنها غير متزامنة، وبالتالي تُرجع `Promise`.
*	`await` توقف التنفيذ داخل دالة `async` حتى يتم تحقيق (resolves) الـ `Promise`.

---

👨‍💻 **2. مثال أساسي على `async/await`**
```javascript
async function fetchData() {
  try {
    const response = await fetch('[https://api.example.com/data](https://api.example.com/data)');
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error('Fetch error:', error);
  }
}

fetchData();
```

---

⚠️ **3. نقاط رئيسية**
*	يمكنك استخدام `await` فقط داخل دوال `async`.
*	استخدم كتل `try/catch` لمعالجة الأخطاء عند استخدام `async/await`.
*	دوال `async` تُرجع دائمًا `Promise`.

---

🧠 **النقاط الرئيسية**
*	`Async/await` تجعل الكود غير المتزامن أسهل في القراءة والكتابة.
*	تعامل دائمًا مع الأخطاء باستخدام `try/catch`.
*	استخدم `await` داخل الدوال المُعلنة بـ `async`.

---
