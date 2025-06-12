### 🛠️ تمرين عملي
**الدالة التي سنختبرها:**
```javascript
// file: user.js
function createUser(username) {
  if (!username || typeof username !== 'string' || username.length < 3) {
    return null; // أرجع null للمدخلات غير الصالحة
  }
  return {
    id: Date.now(),
    username: username.toLowerCase()
  };
}
```
**المهمة:**
1.  أنشئ ملف `user.test.js`.
2.  اكتب مجموعة اختبار (`describe`) لدالة `createUser`.
3.  اكتب حالة اختبار (`it`) تتحقق من أنها تُرجع كائن مستخدم صحيحًا عند إعطائها اسم مستخدم صالح. استخدم `.toEqual()` أو `.toHaveProperty()`.
4.  اكتب حالة اختبار أخرى تتحقق من أنها تُرجع `null` عند إعطائها اسم مستخدم قصيرًا جدًا. استخدم `.toBeNull()`.
5.  اكتب حالة اختبار ثالثة تتحقق من أنها تُرجع `null` إذا لم يتم تمرير أي اسم مستخدم. استخدم `.toBeNull()`.

---
