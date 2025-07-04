## 🧠 الوحدة 2: الخوارزميات الأساسية (Core Algorithms)

### 📘 الدرس 2: أنواع الخوارزميات الأساسية: التكرار، التفرع، والتسلسل

#### 🧠 **ماذا ستتعلم**
* فهم الأنواع الرئيسية للخوارزميات من حيث التحكم في تدفق التنفيذ.
* التعرف على مفهوم التكرار (Loops).
* فهم التفرع (Conditionals).
* التسلسل (Sequence) كأساس لأي خوارزمية.

---
### 🧾 1. ما هو تسلسل الأوامر (Sequence)؟
التسلسل هو أبسط بنية تحكم، وتعني ببساطة تنفيذ التعليمات **خطوة بخطوة**، واحدة تلو الأخرى، بنفس الترتيب الذي كُتبت به. كل خوارزمية تبدأ بتسلسل واضح من الأوامر.

---
### 💡 2. التفرع (Branching / Conditionals)
التفرع يعني **اتخاذ قرار** بناءً على شرط معين. إذا كان الشرط صحيحًا، يتم تنفيذ مجموعة من الأوامر، وإذا لم يكن كذلك، قد يتم تنفيذ مجموعة أخرى أو تخطي المجموعة الأولى.

> 📌 **مثال بالوصف:**
> إذا كانت درجة الطالب 60 أو أكثر ← فهو "ناجح"، وإلا ← فهو "راسب".

**مثال بالكود (`if/else`):**
```javascript
if (grade >= 60) {
  console.log("ناجح");
} else {
  console.log("راسب");
}
```

---
### ⚙️ 3. التكرار (Loop / Iteration)
التكرار يسمح بتنفيذ مجموعة من الخطوات بشكل متكرر طالما أن شرطًا معينًا ما زال متحققًا. يُستخدم التكرار للتعامل مع كميات كبيرة من البيانات أو لتنفيذ مهمة عددًا محددًا من المرات.

**أنواع التكرار الشائعة:**
* `for`
* `while`
* `do…while`

**مثال: طباعة الأرقام من 1 إلى 5:**
```javascript
for(let i = 1; i <= 5; i++) {
  console.log(i);
}
```

---
### 📦 4. كيف ترتبط هذه الأنواع بالخوارزميات؟

| النوع | الوصف | مثال واقعي |
| :--- | :--- | :--- |
| **تسلسل** | تنفيذ خطوة تلو الأخرى بالترتيب. | اتباع خطوات وصفة طبخ بالترتيب. |
| **تفرع** | اتخاذ قرار بناءً على شرط. | اختيار طريق بناءً على حالة حركة المرور. |
| **تكرار** | تكرار خطوات طالما تحقق شرط معين. | تكرار تنظيف طبق حتى يصبح نظيفًا تمامًا. |

---
### 👁️‍🗨️ 5. لماذا فهم هذه الأنواع مهم؟
* تساعدك على كتابة خوارزميات واضحة ومنظمة.
* هي اللبنات الأساسية لكل البرامج والتطبيقات.
* تسهل فهم كيفية تدفق البرنامج وتحديد أماكن المشاكل (Debugging).

---
### 🛠️ جرب بنفسك
اكتب دالة تطبع الأرقام الزوجية فقط بين 1 و 10 باستخدام حلقة `for` وشرط `if`.
```javascript
function printEvenNumbers() {
  // اكتب الكود هنا
}
```

---