# الوحدة 5: وقت تشغيل جافاسكريبت والعمليات الداخلية
**(JavaScript Runtime & Internals)**

## الدرس 5: محرك JavaScript
**(The JavaScript Engine)**

🧠 **ماذا ستتعلم**
* ما هو محرك JavaScript
* مكونات المحرك الرئيسية (Parsing, Compilation, Execution)
* أشهر المحركات المستخدمة اليوم
* كيف تُنفذ JavaScript الكود داخل هذه المحركات
* تقنيات تحسين الأداء مثل JIT

---

### 🧾 1. ما هو محرك JavaScript؟

محرك JavaScript هو البرنامج المسؤول عن **تحليل وتشغيل** كود JavaScript داخل المتصفح أو بيئة أخرى مثل Node.js أو Bun.

📌 عند فتح صفحة ويب أو تشغيل ملف JavaScript، يعمل المحرك على:
1.  تحليل الكود (Parsing)
2.  تحويله إلى تمثيل داخلي (AST)
3.  ترجمته إلى Bytecode أو Machine Code
4.  تنفيذ التعليمات خطوة بخطوة

---

### ⚙️ 2. أشهر محركات JavaScript

| اسم المحرك | يُستخدم في | لغة البرمجة المستخدمة |
| :--- | :--- | :--- |
| **V8** | Google Chrome, Node.js | C++ |
| **SpiderMonkey** | Mozilla Firefox | C/C++ |
| **JavaScriptCore** | Safari (Apple) | C++ |
| **Hermes** | React Native | C++ |
| **Bun Engine** | Bun | Zig |

---

### 🛠️ 3. مكونات محرك JavaScript

كل محرك يحتوي عادةً على هذه الأجزاء:
* **Parser:** يحلل الكود إلى بنية يفهمها الحاسوب (AST).
* **Interpreter:** يترجم الكود إلى تعليمات قابلة للتنفيذ مباشرة.
* **JIT Compiler:** يحوّل الكود إلى لغة الآلة **أثناء التشغيل** لتحسين الأداء.
* **Garbage Collector:** يدير الذاكرة ويحرر الموارد غير المستخدمة.

---

### 🔍 4. كيف يتم تنفيذ الكود؟

مثال على شيفرة بسيطة:
```javascript
function greet(name) {
  return `Hello, ${name}`;
}

console.log(greet("Zaid"));
```
🔎 **خطوات التنفيذ في المحرك:**
* يتم تحليل الكود لبناء AST.
* يتم تحويل `greet` إلى وظيفة داخلية.
* عند استدعاء `greet("Zaid")`، يُضاف إلى المكدس ويتم تنفيذه.
* تُطبع النتيجة في وحدة التحكم.

---

### 🚀 5. ما هو JIT Compiler؟

**JIT (Just-In-Time Compiler)** هو أسلوب يجمع بين **التفسير** و**الترجمة**:
* يبدأ الكود بالتنفيذ مباشرة عبر الـ Interpreter.
* إذا لاحظ المحرك أن بعض الأجزاء تتكرر، يقوم **بترجمتها إلى Machine Code** لتسريع التنفيذ.

💡 هذا هو السبب في أن JavaScript الحديثة أسرع بكثير مما كانت عليه سابقًا.

---

### 👁️‍🗨️ مثال من الواقع

عند استخدامك تطبيق ويب مثل Gmail أو Google Docs، يتم تنفيذ آلاف الأسطر من JavaScript على الفور — وكل هذا يتم بفضل كفاءة محرك V8 وتقنيات JIT وGarbage Collection.

---

### 🔍 حقيقة ممتعة

محرك V8 يقوم بتحسين الكود من تلقاء نفسه! فإذا كنت تكتب كودًا واضحًا ومنظمًا، فإن V8 سيقوم بتحسينه وتشغيله بكفاءة أعلى.

---

### 🚀 ماذا بعد؟

في الدرس الأخير، سنتحدث عن **مكدس المهام، قائمة الانتظار، الحلقة الحدثية (Event Loop)** لفهم كيف تتعامل JavaScript مع العمليات غير المتزامنة (Asynchronous Tasks).

---