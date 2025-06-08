## 🧪 تحدي تدريبي: استخدام المعامل الثلاثي (Ternary Operator)

### 🎯 التحدي:

في محرر JavaScript الخاص بك:

1. قم بالإعلان عن متغير باسم `isMember` واضبطه إما على `true` أو `false`.  
2. أنشئ رسالة باستخدام **المعامل الثلاثي** كالتالي:
   - إذا كانت القيمة `true` → الرسالة: `"Welcome, member!"`
   - إذا كانت القيمة `false` → الرسالة: `"Please sign up."`
3. اطبع الرسالة باستخدام `console.log`.

---

### 💡 تلميحات:

- الصيغة العامة للمعامل الثلاثي:
  ```javascript
  condition ? valueIfTrue : valueIfFalse;

		يمكنك تعيين الناتج إلى متغير أو طباعته مباشرة
	```

✅ الحل النموذجي:

```javascript
let isMember = true;

let message = isMember ? "Welcome, member!" : "Please sign up.";

console.log(message);
```
🧪 جرّب تغيير قيمة isMember إلى false واختبر الرسالة الناتجة!