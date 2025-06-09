# الوحدة 1: نموذج كائن المستند (DOM)

## الدرس 5: اجتياز DOM (DOM Traversal)



🧠 **ماذا ستتعلم**
*	كيفية التنقل بين العناصر في DOM
*	كيفية الوصول إلى العقد الأصل (parent)، والابن (child)، والشقيقة (sibling)
*	كيفية المرور عبر العناصر الأبناء

---

🧭 **1. ما هو اجتياز DOM؟**

بمجرد تحديد عنصر، يمكنك التنقل في DOM للوصول إلى العناصر ذات الصلة — مثل العنصر الأصل، أو الابن، أو الشقيق.

يُطلق على هذا اسم اجتياز DOM.

---

🌳 **2. العناصر الأصل (Parent Elements)**

للحصول على العنصر الأصل لعنصر ما:
```javascript
element.parentElement
```

مثال:
```html
<div id="parent">
  <p id="child">Hi!</p>
</div>
```
```javascript
let child = document.getElementById("child");
let parent = child.parentElement;

console.log(parent.id); // الناتج: "parent"
```

---

👶 **3. أبناء العنصر (Children of an Element)**

للوصول إلى جميع الأبناء:
```javascript
element.children
```

للحصول على أول أو آخر ابن:
```javascript
element.firstElementChild
element.lastElementChild
```

مثال:
```html
<ul id="groceries">
  <li>Apples</li>
  <li>Bananas</li>
</ul>
```
```javascript
let list = document.getElementById("groceries");
console.log(list.children.length); // الناتج: 2
console.log(list.firstElementChild.textContent); // الناتج: "Apples"
```

---

👯 **4. العناصر الشقيقة (Sibling Elements)**

للتنقل بين العناصر الشقيقة:
```javascript
element.nextElementSibling
element.previousElementSibling
```

مثال:
```html
<p id="one">First</p>
<p id="two">Second</p>
<p id="three">Third</p>
```
```javascript
let second = document.getElementById("two");
console.log(second.previousElementSibling.textContent); // الناتج: "First"
console.log(second.nextElementSibling.textContent);     // الناتج: "Third"
```

---

🔁 **5. المرور عبر الأبناء**

يمكنك المرور عبر `element.children` باستخدام حلقة `for...of`:
```javascript
let list = document.getElementById("groceries"); // بافتراض استخدام قائمة "groceries" من المثال السابق

for (let item of list.children) {
  console.log(item.textContent);
}
// الناتج:
// Apples
// Bananas
```

---

🔄 **6. ملخص سريع: التنقل في DOM**

| الإجراء             | الكود                             |
| :----------------- | :-------------------------------- |
| الانتقال إلى الأصل | `element.parentElement`           |
| الحصول على الأبناء | `element.children`                |
| الابن الأول/الأخير  | `firstElementChild`, `lastElementChild` |
| الشقيق التالي      | `element.nextElementSibling`      |
| الشقيق السابق     | `element.previousElementSibling`  |


---

🧠 **النقاط الرئيسية**
*	اجتياز DOM يساعدك على التنقل في المستند من أي نقطة بداية.
*	استخدم `.parentElement`، `.children`، `.nextElementSibling`، إلخ، للتنقل.
*	المرور عبر الأبناء مفيد للتحديثات أو الفحوصات المجمعة.

