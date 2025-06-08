# الوحدة 1: نموذج كائن المستند (DOM)

## الدرس 2: تحديد العناصر


🧠 **ماذا ستتعلم**
*	كيفية تحديد عناصر HTML باستخدام جافاسكريبت
*	الفرق بين `getElementById`، `querySelector`، وطرق التحديد الأخرى
*	أفضل الممارسات للتعامل مع تحديدات DOM

---

📄 **1. لماذا يعد تحديد العناصر مهمًا؟**

قبل أن تتمكن من تغيير أي شيء على الصفحة — النص، الأنماط، المحتوى — تحتاج إلى تحديد عنصر HTML الذي تريد العمل معه.

توفر لك جافاسكريبت دوال قوية للقيام بذلك.

---

🛠️ **2. دوال التحديد الشائعة**

| الدالة (Method)                 | الوصف                                                          |
|-------------------------------|-----------------------------------------------------------------|
| `getElementById("id")`        | تحدد عنصرًا واحدًا بواسطة مُعرّفه (ID)                           |
| `getElementsByClassName("class")` | تُرجع مجموعة من العناصر التي تحمل ذلك الصنف (class)            |
| `getElementsByTagName("tag")` | تُرجع جميع العناصر التي تحمل اسم الوسم (tag) ذاك                 |
| `querySelector("selector")`   | تحدد أول تطابق باستخدام مُحدِّد بنمط CSS                         |
| `querySelectorAll("selector")`| تحدد جميع التطابقات باستخدام مُحدِّد بنمط CSS                    |

---

🔍 **3. جرب بنفسك – التحديد بواسطة ID**

HTML:
```html
<h2 id="main-title">Hello!</h2>
```

JavaScript:
```javascript
let title = document.getElementById("main-title");
console.log(title.textContent); // الناتج: Hello!
```

---

🔍 **4. جرب بنفسك – التحديد بواسطة الصنف (Class) والوسم (Tag)**

HTML:
```html
<p class="message">First</p>
<p class="message">Second</p>
```

JavaScript:
```javascript
let messages = document.getElementsByClassName("message");
console.log(messages[0].textContent); // الناتج: First
```
ملاحظة: تُرجع `getElementsByClassName` مجموعة `HTMLCollection` حية – وهي تشبه المصفوفة، ولكنها ليست كذلك تمامًا.

---

🔍 **5. استخدام `querySelector`**

HTML:
```html
<div class="card">
  <p>Card content</p>
</div>
```

JavaScript:
```javascript
let card = document.querySelector(".card"); // مُحدِّد بنمط CSS
console.log(card.textContent); // الناتج: Card content
```

---

📚 **6. تحديد عناصر متعددة باستخدام `querySelectorAll`**

HTML:
```html
<ul>
  <li>Apple</li>
  <li>Banana</li>
</ul>
```

JavaScript:
```javascript
let items = document.querySelectorAll("li");
items.forEach(item => {
  console.log(item.textContent);
});
```

✅ `querySelectorAll()` تعطيك `NodeList` — وهي تشبه المصفوفة، ويمكنك استخدام `.forEach()` معها.

---

⚠️ **7. احذر مما تحدده**

إذا استخدمت `getElementById("main")` ولم يكن هناك عنصر بهذا الـ ID، فسوف تُرجع `null`.
لذا تحقق دائمًا:
```javascript
let element = document.getElementById("main");
if (element) {
  console.log("Found it!");
}
```

---


🚀 **ماذا بعد؟**

الآن بعد أن أصبحت قادرًا على تحديد العناصر، دعنا نتعلم كيفية تغييرها — نصوصها، وأنماطها، وحتى سماتها. 
التالي: الدرس 3: تعديل النصوص والأنماط.

---