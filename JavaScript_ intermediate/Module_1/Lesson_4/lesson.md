# الوحدة 1: نموذج كائن المستند (DOM)

## الدرس 4: إنشاء العناصر وإزالتها

---

🧠 **ماذا ستتعلم**
*	كيفية إنشاء عناصر HTML جديدة باستخدام جافاسكريبت
*	كيفية إدراج العناصر في DOM
*	كيفية إزالة العناصر من DOM

---

🧱 **1. إنشاء عنصر**

لإنشاء عنصر HTML في جافاسكريبت، استخدم:
```javascript
document.createElement("tagName");
```

مثال:
```javascript
let newDiv = document.createElement("div");
```
هذا ينشئ عنصر `<div>` جديد، ولكنه ليس في DOM بعد.

---

📌 **2. إضافة محتوى إلى العنصر**

يمكنك إضافة نص أو HTML داخلي إليه:
```javascript
newDiv.textContent = "Hello, I’m new here!";
```

أو:
```javascript
newDiv.innerHTML = "<strong>Bold move!</strong>";
```

---

📥 **3. إضافة العنصر إلى الصفحة**

لإدراج العنصر في المستند:
```javascript
document.body.appendChild(newDiv);
```
هذا يضيف العنصر في نهاية الوسم `<body>`.

يمكنك أيضًا الإلحاق بعنصر معين:
```html
<ul id="list"></ul>
```
```javascript
let list = document.getElementById("list");
let item = document.createElement("li");
item.textContent = "New list item";
list.appendChild(item);
```

---

🧹 **4. إزالة عنصر**

لإزالة عنصر من الصفحة:
```javascript
element.remove();
```

مثال:
```html
<p id="bye">Goodbye!</p>
```
```javascript
let paragraph = document.getElementById("bye");
paragraph.remove();
```
✅ فقط تأكد من أنك قمت بتحديد العنصر قبل محاولة إزالته.

---

🔄 **5. الإدراج في مواضع محددة**

يمكنك أيضًا استخدام:
*	`prepend()` — يضيف كأول عنصر ابن
*	`insertBefore(newNode, referenceNode)` — يضيف قبل عنصر محدد

مثال:
```javascript
let parent = document.getElementById("container");
let box = document.createElement("div");
box.textContent = "I'm inserted!";
parent.prepend(box); // يضيف إلى الأعلى
```

---



🧠 **النقاط الرئيسية**
*	استخدم `document.createElement()` لإنشاء عناصر جديدة.
*	استخدم `appendChild()`، `prepend()`، أو `insertBefore()` لوضعها.
*	استخدم `.remove()` لحذف العناصر من DOM.

---

🚀 **ماذا بعد؟**

الآن بعد أن أصبحت قادرًا على إضافة وإزالة العناصر، دعنا نتعلم كيفية التنقل داخل DOM — مثل الوصول إلى العناصر الأصل، والابن، والشقيق. هذا ما سنتناوله في الدرس 5: اجتياز DOM.