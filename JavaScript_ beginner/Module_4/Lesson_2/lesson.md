# الوحدة 4: المصفوفات والكائنات

## الدرس 2: دوال المصفوفات الشائعة (push، pop، slice، splice)

🧠 **ماذا ستتعلم**
*	كيفية استخدام `()push.` و `()pop.`
*	كيفية استخدام `()slice.` لنسخ أجزاء من مصفوفة
*	كيفية استخدام `()splice.` لإدراج أو إزالة أو استبدال العناصر
*	كيف تؤثر هذه الدوال على المصفوفة الأصلية

---

➕ **1. `push()`: الإضافة إلى النهاية**

تضيف عنصرًا جديدًا إلى نهاية المصفوفة.
```javascript
let fruits = ["apple", "banana"];
fruits.push("cherry");
console.log(fruits); // الناتج: ["apple", "banana", "cherry"]
```

---

➖ **2. `pop()`: الإزالة من النهاية**

تزيل العنصر الأخير من المصفوفة وتُرجعه.
```javascript
let animals = ["dog", "cat", "parrot"];
let removed = animals.pop();
console.log(removed); // الناتج: "parrot"
console.log(animals); // الناتج: ["dog", "cat"]
```

---

✂️ **3. `slice()`: نسخ جزء من المصفوفة**

تُرجع نسخة سطحية (shallow copy) لجزء من المصفوفة.
**لا تُغير** المصفوفة الأصلية.
```javascript
let colors = ["red", "green", "blue", "yellow"];
let sliced = colors.slice(1, 3);
console.log(sliced); // الناتج: ["green", "blue"]
console.log(colors); // الناتج: ["red", "green", "blue", "yellow"]
```
البنية: `array.slice(startIndex, endIndex)`
`endIndex` (فهرس النهاية) غير مشمول.

---

🔁 **4. `splice()`: إضافة/إزالة العناصر**

يمكنها إضافة أو إزالة أو استبدال العناصر.
**تُغير** المصفوفة الأصلية.

🧹 **إزالة العناصر:**
```javascript
let nums = [10, 20, 30, 40];
nums.splice(1, 2); // ابدأ من الفهرس 1، أزل عنصرين
console.log(nums); // الناتج: [10, 40]
```

➕ **إدراج العناصر:**
```javascript
let pets = ["dog", "cat"];
pets.splice(1, 0, "parrot"); // (لا يتم إزالة أي عناصر (0)، يتم إدراج "parrot" في الفهرس 1)
console.log(pets); // الناتج: ["dog", "parrot", "cat"]
```

🔄 **استبدال العناصر:**
```javascript
let tools = ["hammer", "wrench", "screwdriver"];
tools.splice(1, 1, "drill"); // استبدل "wrench" بـ "drill"
console.log(tools); // الناتج: ["hammer", "drill", "screwdriver"]
```

---

🧪 **جرب بنفسك**
```javascript
let scores = [100, 90, 80, 70];
let topTwo = scores.slice(0, 2);
console.log(topTwo); // الناتج: [100, 90]

scores.splice(2, 1, 85); // في الفهرس 2، أزل عنصرًا واحدًا، وأضف 85
console.log(scores); // الناتج: [100, 90, 85, 70]
```

---

🧠 **النقاط الرئيسية**
*	`.push()` تضيف إلى النهاية.
*	`.pop()` تزيل من النهاية.
*	`.slice()` تنسخ جزءًا من المصفوفة (غير مُدمرة).
*	`.splice()` تضيف/تزيل/تستبدل العناصر (مُدمرة).

---