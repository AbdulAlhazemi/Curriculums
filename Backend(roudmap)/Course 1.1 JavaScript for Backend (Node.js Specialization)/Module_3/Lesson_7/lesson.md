### 📘 الدرس 7: العمل مع وحدات Node.js (Modules) - مراجعة

#### 🧠 ماذا ستتعلم؟
* مفهوم الوحدات (Modules) في Node.js.
* الفرق بين **CommonJS** و **ES Modules**.
* كيفية إنشاء وحدة خاصة بك واستخدامها.
* كيفية استيراد وتصدير الوظائف والمتغيرات بين الملفات.

---
### 1. ما هي الوحدات في Node.js؟
الوحدات (Modules) هي أجزاء من الكود يمكنك فصلها في ملفات مختلفة وإعادة استخدامها في ملفات أخرى. هذا يساعد في تنظيم الكود وجعله أكثر قابلية للصيانة.

---
### 2. نظام الوحدات في Node.js: CommonJS و ES Modules
* **CommonJS** هو النظام التقليدي في Node.js، يستخدم `require()` للاستيراد و`module.exports` للتصدير.
* **ES Modules (ESM)** هو النظام الحديث الذي يستخدم `import` و `export`، وهو متوافق مع جافاسكريبت في المتصفحات.

---
### 3. استخدام CommonJS

**تصدير:**
```javascript
// math.js
function sum(a, b) {
  return a + b;
}

module.exports = { sum };
```

**استيراد:**
```javascript
// app.js
const math = require('./math');

console.log(math.sum(5, 3)); // 8
```

---
### 4. استخدام ES Modules (مع تفعيل `type: "module"` في package.json)

**تصدير:**
```javascript
// math.mjs
export function sum(a, b) {
  return a + b;
}
```

**استيراد:**
```javascript
// app.mjs
import { sum } from './math.mjs';

console.log(sum(5, 3)); // 8
```

---
### 5. إنشاء وحدة خاصة بك
يمكنك كتابة دوال أو متغيرات في ملف ثم تصديرها لاستخدامها في ملفات أخرى، مما يسهل إعادة استخدام الكود.

---

