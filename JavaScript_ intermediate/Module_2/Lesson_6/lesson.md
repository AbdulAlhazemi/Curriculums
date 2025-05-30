# الوحدة 2: الأحداث والتفاعلية

## الدرس 6: أساسيات تأخير التنفيذ (Debouncing) وتنظيم التكرار (Throttling)

---

🧠 **ماذا ستتعلم**
*	ماذا يعني تأخير التنفيذ (debouncing) وتنظيم التكرار (throttling) في جافاسكريبت
*	لماذا هي مهمة للأداء وتجربة المستخدم
*	كيفية تنفيذ دوال بسيطة لتأخير التنفيذ وتنظيم التكرار

---

🚀 **1. المشكلة: كثرة الأحداث**

بعض الأحداث مثل `scroll`، `resize`، أو `input` يمكن أن تُطلق عشرات المرات في الثانية. هذا يمكن أن:
*	يبطئ تطبيقك
*	يثقل كاهل المتصفح
*	يجعل واجهات المستخدم بطيئة (laggy)

نحتاج إلى طريقة للحد من عدد مرات تشغيل الدالة.

---

💡 **2. ما هو تأخير التنفيذ (Debouncing)؟**

تأخير التنفيذ (Debouncing) يؤخر تشغيل دالة ما حتى حدوث توقف مؤقت في تدفق الأحداث.

فكر في شخص يكتب في شريط بحث — لا تريد إطلاق البحث بعد كل ضغطة مفتاح. تنتظر حتى يتوقف عن الكتابة لثانية واحدة.

---

✍️ **مثال: دالة تأخير التنفيذ (Debounce)**
```javascript
function debounce(callback, delay) {
  let timeout;
  return function () {
    clearTimeout(timeout);
    timeout = setTimeout(callback, delay);
  };
}

const logInput = () => {
  console.log("Input processed!");
};

const debouncedLog = debounce(logInput, 500);

document.querySelector("#search").addEventListener("input", debouncedLog);
```
📝 سيتم تشغيل دالة `logInput` فقط بعد مرور 500 مللي ثانية من عدم الكتابة.

---

⚡ **3. ما هو تنظيم التكرار (Throttling)؟**

تنظيم التكرار (Throttling) يضمن تشغيل الدالة مرة واحدة فقط كل X مللي ثانية، بغض النظر عن عدد مرات حدوث الحدث.

هذا مفيد لأشياء مثل تتبع موضع التمرير.

---

✍️ **مثال: دالة تنظيم التكرار (Throttle)**
```javascript
function throttle(callback, interval) {
  let lastTime = 0;
  return function () {
    const now = Date.now();
    if (now - lastTime >= interval) {
      callback();
      lastTime = now;
    }
  };
}

const logScroll = () => {
  console.log("Scroll event");
};

const throttledScroll = throttle(logScroll, 1000);

window.addEventListener("scroll", throttledScroll);
```
📝 هذا يسجل مرة واحدة على الأكثر في الثانية، بغض النظر عن سرعة التمرير.

---

📊 **4. متى نستخدم كلاً منهما**

| حالة الاستخدام             | Debounce (تأخير) 🕓 | Throttle (تنظيم) ⚡ |
| :------------------------ | :----------------- | :----------------- |
| حقل إدخال البحث           | ✅ نعم             | 🚫 لا              |
| تغيير حجم النافذة        | ✅ نعم             | ✅ ربما            |
| تتبع التمرير             | 🚫 لا              | ✅ نعم             |
| التحقق من حقول النموذج   | ✅ نعم             | 🚫 لا              |

---

🧠 **النقاط الرئيسية**
*	تأخير التنفيذ (Debounce) ينتظر توقفًا مؤقتًا في الأحداث.
*	تنظيم التكرار (Throttle) يحد من عدد مرات تشغيل الدالة.
*	هذه التقنيات تحافظ على سرعة وكفاءة تطبيقاتك.

---

✅ بهذا نختتم الوحدة 2: الأحداث والتفاعلية!