### 🛠️ تمرين عملي
1.  أنشئ ملفًا `logger.js` يحتوي على دالة `log(message)` تقوم بطباعة الرسالة في الطرفية.
2.  أنشئ ملفًا `calculator.js` يحتوي على دالة `add(a, b)`. يجب أن تستدعي هذه الدالة `logger.log('adding numbers')` قبل أن تُرجع المجموع.
3.  أنشئ ملف اختبار `calculator.test.js`.
4.  استخدم `jest.mock('./logger.js')` لمحاكاة وحدة التسجيل.
5.  اكتب حالة اختبار تستدعي `add(5, 7)`.
6.  استخدم `expect().toBe()` للتأكد من أن النتيجة هي `12`.
7.  الأهم من ذلك، استخدم `expect(log).toHaveBeenCalledWith('adding numbers')` للتأكد من أن دالة `add` قامت باستدعاء الـ logger بالرسالة الصحيحة.

---
