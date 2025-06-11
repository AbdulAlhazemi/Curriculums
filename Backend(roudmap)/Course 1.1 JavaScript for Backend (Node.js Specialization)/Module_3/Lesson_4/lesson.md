## 🟩 الوحدة 3: أساسيات Node.js

### 📘 الدرس 4: العمل مع الوحدات في Node.js (CommonJS vs ES Modules)

#### 🧠 ماذا ستتعلم؟
* مفهوم الوحدات (Modules) في Node.js ولماذا نحتاجها.
* الفرق بين نظام **CommonJS** (`require`/`module.exports`) ونظام **ES Modules** (`import`/`export`).
* كيفية إنشاء وحدة خاصة بك واستخدامها.
* مميزات وقيود كل نظام.

---
#### 1. ما هي الوحدات (Modules)؟
الوحدات تسمح لك بتقسيم الكود إلى ملفات صغيرة، كل ملف يحتوي على جزء من التطبيق. هذا يساعد في **تنظيم الكود** و**إعادة استخدامه** بسهولة.

---
#### 2. CommonJS: النظام الافتراضي في Node.js
* تستخدم `require()` لاستيراد الوحدات.
* تستخدم `module.exports` لتصدير الوظائف أو المتغيرات.

**مثال:**
```javascript
// math.js
function add(a, b) {
  return a + b;
}
module.exports = add;

// main.js
const add = require('./math');
console.log(add(2, 3));  // 5
```

---
#### 3. ES Modules: النظام الحديث
* يستخدم `import` و `export`.
* يحتاج إلى ضبط `package.json` أو استخدام امتداد `.mjs`.
* أكثر توافقاً مع المتصفحات الحديثة وأدوات البناء.

**مثال:**
```javascript
// math.mjs
export function add(a, b) {
  return a + b;
}

// main.mjs
import { add } from './math.mjs';
console.log(add(2, 3));  // 5
```

---
#### 4. كيف تختار بينهما؟

| المعيار | CommonJS | ES Modules |
| :--- | :--- | :--- |
| **التوافق** | Node.js فقط | Node.js والمتصفحات |
| **طريقة الاستيراد**| `require` | `import` |
| **التصدير** | `module.exports`| `export` |
| **الدعم** | موجود في كل إصدارات Node | حديث، يحتاج إعدادات |

---
#### 5. إنشاء وحدة خاصة بك (مثال)
```javascript
// greetings.js
function sayHello(name) {
  return `مرحباً، ${name}!`;
}
module.exports = sayHello;

// app.js
const sayHello = require('./greetings');
console.log(sayHello('أحمد'));
```

---