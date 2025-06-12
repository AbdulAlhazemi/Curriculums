### 🛠️ تمرين عملي
خذ الدالة التالية واجعلها أكثر دفاعية.
**الكود الأصلي:**
```javascript
function getInitials(fullName) {
  const parts = fullName.split(' ');
  const firstName = parts[0];
  const lastName = parts[parts.length - 1];
  return firstName[0].toUpperCase() + lastName[0].toUpperCase();
}
```
**المشاكل المحتملة:** ماذا لو كان `fullName` هو `null` أو `undefined`؟ ماذا لو كان سلسلة نصية فارغة؟ ماذا لو كان اسمًا واحدًا فقط؟

* **المهمة:** أعد كتابة هذه الدالة لتتعامل مع هذه الحالات بأمان (على سبيل المثال، بإرجاع سلسلة فارغة أو إطلاق خطأ مناسب).

---
