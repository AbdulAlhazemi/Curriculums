## 🧪 تحدي تدريبي: تحويل الأنواع (Type Coercion) في JavaScript

### 🎯 التحدي:

في محرر JavaScript الخاص بك:

1. أنشئ متغيرًا يحمل السلسلة النصية `"100"`.  
2. حوّل هذه السلسلة إلى رقم باستخدام طريقة التحويل المناسبة، واطبع الناتج ونوعه.  
3. أضف رقمًا (مثلاً 50) إلى السلسلة النصية الأصلية **بدون تحويلها أولًا**، واطبع الناتج.  
4. حاول طرح رقم (مثلاً 30) من السلسلة النصية الأصلية ولاحظ الناتج.

---

### 💡 تلميحات:

- استخدم `()Number` أو `()parseInt` لتحويل السلسلة النصية إلى رقم.  
- عند جمع رقم مع سلسلة نصية، سيحدث إكراه تلقائي إلى نص (concatenation).  
- عند طرح رقم من سلسلة نصية، JavaScript تحاول تحويل السلسلة إلى رقم تلقائيًا.

---

### ✅ الحل النموذجي:

```javascript
let strNum = "100";

// تحويل النص إلى رقم
let num = Number(strNum);
console.log(num);           // 100
console.log(typeof num);    // "number"

// جمع رقم مع نص (concatination)
let concatResult = strNum + 50;
console.log(concatResult);  // "10050"
console.log(typeof concatResult); // "string"

// طرح رقم من نص (JavaScript يحول النص لرقم تلقائيًا)
let subtractionResult = strNum - 30;
console.log(subtractionResult); // 70
console.log(typeof subtractionResult); // "number"
```