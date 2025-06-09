# الوحدة 1: نموذج كائن المستند (DOM)

## الدرس 3: تعديل النصوص والأنماط


🧠 **ماذا ستتعلم**
*	كيفية تغيير محتوى النص في عناصر HTML باستخدام جافاسكريبت
*	كيفية تحديث أنماط العناصر ديناميكيًا
*	الفرق بين `textContent`، `innerText`، و `innerHTML`

---

📄 **1. تغيير محتوى النص**

يمكنك تغيير النص داخل عنصر HTML باستخدام:
```javascript
element.textContent = "New Text!";
```

مثال:

HTML:
```html
<h2 id="title">Original Title</h2>
```

JavaScript:
```javascript
let title = document.getElementById("title");
title.textContent = "Updated Title";
```

🧠 **ماذا تفعل `textContent`؟**
تقوم بتعيين أو الحصول على النص داخل العنصر، متجاهلة أي وسوم HTML بداخله.

---

🆚 **2. `textContent` مقابل `innerText` مقابل `innerHTML`**

| الخاصية     | وظيفتها                                           |
| :---------- | :------------------------------------------------ |
| `textContent` | تجلب/تُعين كل النص، بما في ذلك المحتوى المخفي     |
| `innerText`   | تجلب/تُعين النص المرئي فقط (تستثني النص المخفي)  |
| `innerHTML`   | تجلب/تُعين محتوى HTML (وليس النص فقط!)           |

مثال:
```html
<p id="demo"><strong>Hello</strong> world</p>
```

```javascript
let p = document.getElementById("demo");

console.log(p.textContent); // الناتج: "Hello world"
console.log(p.innerText);   // الناتج: "Hello world"
console.log(p.innerHTML);   // الناتج: "<strong>Hello</strong> world"
```

---

🎨 **3. تغيير الأنماط باستخدام `.style`**

كل عنصر HTML لديه خاصية `style` يمكنك استخدامها لتغيير مظهره.

HTML:
```html
<p id="colorful">Color me!</p>
```

JavaScript:
```javascript
let para = document.getElementById("colorful");
para.style.color = "red";
para.style.fontSize = "20px";
para.style.backgroundColor = "lightyellow";
```

⚠️ استخدم `camelCase` لخصائص CSS متعددة الكلمات:
*	`background-color` → `backgroundColor`
*	`font-size` → `fontSize`

---

🔄 **4. تغيير أنماط متعددة**

يمكنك تطبيق أنماط متعددة بهذا الشكل:
```javascript
element.style.cssText = "color: green; font-weight: bold; padding: 10px;";
```

---


🧠 **النقاط الرئيسية**
*	استخدم `.textContent` لتغيير نص العنصر بأمان.
*	استخدم `.innerHTML` عندما تحتاج إلى تضمين أو تحديث وسوم HTML.
*	قم بتنسيق العناصر مباشرة باستخدام `.style.propertyName = "value"`.


---