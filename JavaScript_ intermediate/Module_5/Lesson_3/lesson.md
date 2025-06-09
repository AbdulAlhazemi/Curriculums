 # الوحدة 5: JSON والتعامل مع واجهات برمجة التطبيقات (APIs)

## الدرس 3: جلب البيانات باستخدام `()fetch`


🧠 **ماذا ستتعلم**
*	ما هي واجهة برمجة التطبيقات `()fetch` ولماذا هي مهمة
*	كيفية إجراء طلبات HTTP باستخدام `()fetch`
*	التعامل مع الاستجابات والأخطاء
*	التعامل مع بيانات JSON من واجهات برمجة التطبيقات (APIs)

---

🔍 **1. ما هي `()fetch`؟**

تُستخدم `()fetch` لإجراء طلبات الشبكة في JavaScript، وهي واجهة برمجة تطبيقات (API) حديثة تُرجع `Promise` يتم تحقيقه عند استلام الاستجابة بنجاح.


---

👨‍💻 **2. طلب `fetch` أساسي**

إليك كيفية جلب البيانات من عنوان URL:
```javascript
fetch('[https://api.example.com/data](https://api.example.com/data)')
  .then(response => response.json())  // تحليل JSON من الاستجابة
  .then(data => {
    console.log(data);  // التعامل مع البيانات
  })
  .catch(error => {
    console.error('Error:', error);  // التعامل مع الأخطاء
  });
```
*	`fetch()` تُرجع `Promise`.
*	`.then(response => response.json())` تقوم بتحليل جسم الاستجابة بصيغة JSON.
*	`.catch()` تتعامل مع أخطاء الشبكة أو التحليل.

---

⚠️ **3. ملاحظات هامة**
*	`fetch()` لا ترفض (reject) الـ `Promise` عند حدوث أخطاء HTTP (مثل 404 أو 500). يجب عليك التحقق من `response.ok` بنفسك.
*	للتعامل مع الأخطاء:
```javascript
fetch('[https://api.example.com/data](https://api.example.com/data)')
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json();
  })
  .then(data => {
    console.log(data);
  })
  .catch(error => {
    console.error('Fetch error:', error);
  });
```


---

🧠 **النقاط الرئيسية**
*	تُستخدم `()fetch` لإجراء طلبات HTTP وتُرجع `Promise`.
*	استخدم `()response.json` لتحليل أجسام الاستجابة بصيغة JSON.
*	تحقق دائمًا من `response.ok` للتعامل مع أخطاء HTTP.

---