## 🧪 تحدي تدريبي: الدوال (Functions) في JavaScript

### 🎯 المطلوب:

1. أنشئ **تعريف دالة (Function Declaration)** باسم `greetUser` تقوم بطباعة `"Welcome back!"`
2. أنشئ **تعبير دالة (Function Expression)** باسم `logOutUser` تقوم بطباعة `"Goodbye!"`
3. قم **باستدعاء كلتا الدالتين** لطباعة النتائج.

---

### ✅ الحل النموذجي:

```javascript
// تعريف دالة
function greetUser() {
  console.log("Welcome back!");
}

// تعبير دالة
const logOutUser = function() {
  console.log("Goodbye!");
}

// استدعاء الدالتين
greetUser();
logOutUser();
```
💡 ملاحظات:

	•	تعريف الدالة يمكن استدعاؤه قبل تعريفه في الكود بسبب خاصية “الرفع” (Hoisting).

	•	تعبير الدالة لا يمكن استدعاؤه قبل تعريفه، لأنه يُخزن في متغير.