# الوحدة 5: JSON والتعامل مع واجهات برمجة التطبيقات (APIs)

## الدرس 4: التعامل مع الـ Promises ودالة `()then.`


🧠 **ماذا ستتعلم**
*	ما هي الـ Promises (الوعود) في جافاسكريبت
*	كيف تعمل دالتا `()then.` و `()catch.` للتعامل مع الكود غير المتزامن
*	كتابة سلاسل Promises نظيفة وسهلة الإدارة

---

🔍 **1. ما هي الـ Promises (الوعود)؟**

تمثل الـ Promises الإكمال النهائي (أو الفشل) لعملية غير متزامنة وقيمتها الناتجة.
*	**معلّق (Pending):** الحالة الأولية، لم يتم الوفاء به ولا رفضه
*	**تم الوفاء به (Fulfilled):** اكتملت العملية بنجاح
*	**تم رفضه (Rejected):** فشلت العملية

---

👨‍💻 **2. استخدام `()then.` و `()catch.`**

تعمل دالة `()then.` بعد أن يتم الوفاء بالـ Promise وتستقبل النتيجة.

تعمل دالة `()catch.` إذا تم رفض الـ Promise وتستقبل الخطأ.

مثال:
```javascript
fetch('[https://api.example.com/data](https://api.example.com/data)')
  .then(response => response.json())
  .then(data => {
    console.log('Data:', data);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

---

⚠️ **3. تسلسل الـ Promises**

يمكنك تسلسل عدة استدعاءات لـ `()then.` لمعالجة البيانات خطوة بخطوة:
```javascript
fetch('[https://api.example.com/data](https://api.example.com/data)')
  .then(response => response.json())
  .then(data => {
    return data.results;
  })
  .then(results => {
    console.log('Results:', results);
  })
  .catch(error => {
    console.error('Fetch error:', error);
  });
```

---

🧠 **النقاط الرئيسية**
*	الـ Promises تدير العمليات غير المتزامنة.
*	استخدم `()then.` للنجاح و `()catch.` للأخطاء.
*	تسلسل الـ Promises يتيح لك معالجة النتائج غير المتزامنة خطوة بخطوة.

---