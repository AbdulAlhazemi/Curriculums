Of course, here is Lesson 4 on Modularization, formatted in Markdown.

# الوحدة 7: أنماط كتابة الكود المتقدمة
**(Advanced Code Patterns)**

## الدرس 4: تنظيم الكود باستخدام الوحدات (Modularization)

🧠 **ماذا ستتعلم**
* أهمية تنظيم الكود وتقسيمه إلى وحدات صغيرة.
* كيف تساعد الوحدات في تحسين القابلية للصيانة وإعادة الاستخدام.
* استخدام `export` و `import` في JavaScript.
* أمثلة عملية على إنشاء واستخدام الوحدات.

---

### 🧾 1. ما هو التنظيم باستخدام الوحدات؟
تنظيم الكود باستخدام الوحدات يعني تقسيم البرنامج إلى أجزاء صغيرة (وحدات أو **Modules**) كل منها مسؤول عن وظيفة معينة. هذا يجعل الكود أسهل في الفهم، الصيانة، والتطوير.

---

### 🧠 2. فوائد تنظيم الكود إلى وحدات
* فصل الاهتمامات (**Separation of Concerns**).
* إعادة استخدام الكود بين الملفات والمشاريع.
* تقليل التعقيد.
* تسهيل التعاون بين المطورين.

---

### 🔧 3. كيفية إنشاء وحدة (Module) في JavaScript

#### تصدير (Export) من ملف `module.js`:
```javascript
// module.js
export function greet(name) {
  return `مرحباً، ${name}!`;
}

export const PI = 3.1416;
```

#### استيراد (Import) في ملف آخر:
```javascript
// main.js
import { greet, PI } from './module.js';

console.log(greet('علي')); // مرحباً، علي!
console.log(PI); // 3.1416
```

---

### ⚙️ 4. أنواع التصدير
* **تصدير مسمى (Named Export):**
    ```javascript
    export function foo() {}
    export const bar = 123;
    ```
* **تصدير افتراضي (Default Export):**
    ```javascript
    export default function baz() {}
    ```
    ويتم الاستيراد بهذه الطريقة:
    ```javascript
    import baz from './module.js';
    ```

---

### 🚀 5. متى تستخدم الوحدات؟
* عند كتابة برامج كبيرة.
* لتقسيم الكود حسب الوظائف.
* لتحسين إعادة استخدام الكود.
* لجعل المشروع أكثر تنظيمًا.

---

### 🚀 ماذا بعد؟
في الدرس القادم سنتحدث عن الفرق بين **التكوين (Composition)** و**الوراثة (Inheritance)** في البرمجة الكائنية.

---
