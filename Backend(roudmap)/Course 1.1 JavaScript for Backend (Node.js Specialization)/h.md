## الدرس 1: مراجعة متقدمة لجافاسكريبت (ES6+ Features)

مرحباً بك في هذا الدرس! سنقوم بمراجعة بعض المفاهيم والميزات المتقدمة في جافاسكريبت (ECMAScript 6 وما بعدها) والتي تعتبر أساسية لتطوير الواجهات الخلفية باستخدام Node.js.

---

### 1. الدوال السهمية (Arrow Functions)

الدوال السهمية تقدم صيغة مختصرة لتعريف الدوال. من أبرز ميزاتها أنها لا تقوم بربط قيمة `this` الخاصة بها، بل ترثها من السياق (scope) المحيط بها.

**الصيغة العامة:**

```javascript
// دالة سهمية بسيطة لجمع رقمين
const add = (a, b) => a + b;

// دالة سهمية متعددة الأسطر
const greet = (name) => {
  const message = `Hello, ${name}!`; // النص الناتج بالإنجليزية
  return message;
};

console.log(add(5, 3)); // Output: 8
console.log(greet("World")); // Output: Hello, World!
```

**مثال مع `this`:**

في الدوال التقليدية، قيمة `this` تعتمد على كيفية استدعاء الدالة. أما الدوال السهمية، فتستخدم قيمة `this` من السياق الذي عُرِّفت فيه.

```javascript
function Person() {
  this.age = 0;

  setInterval(() => {
    this.age++; // `this` هنا تشير إلى كائن Person بشكل صحيح
    console.log(this.age);
  }, 1000);
}

const p = new Person();
// سيقوم هذا الكود بطباعة العمر المتزايد كل ثانية
```

لو استخدمنا دالة تقليدية داخل `setInterval` بدون `bind` أو متغير وسيط، لكانت `this` تشير إلى الكائن العام (window في المتصفح أو global في Node.js).

---

### 2. تفكيك الهياكل (Destructuring)

تفكيك الهياكل هو تعبير جافاسكريبت يسمح لك بتفريغ قيم من المصفوفات، أو خصائص من الكائنات، إلى متغيرات مميزة.

#### أ. تفكيك الكائنات (Object Destructuring)

```javascript
const user = {
  firstName: "Ahmed",
  lastName: "Ali",
  city: "Riyadh"
};

// استخراج الخصائص إلى متغيرات بنفس الاسم
const { firstName, city } = user;
console.log(firstName); // Output: Ahmed
console.log(city); // Output: Riyadh

// استخراج مع تغيير اسم المتغير
const { lastName: familyName } = user;
console.log(familyName); // Output: Ali

// تحديد قيم افتراضية
const { country = "Saudi Arabia" } = user; // country غير موجود في الكائن user، لذا سيتم استخدام القيمة الافتراضية
console.log(country); // Output: Saudi Arabia
```

#### ب. تفكيك المصفوفات (Array Destructuring)

```javascript
const colors = ["Red", "Green", "Blue"];

const [firstColor, secondColor] = colors;
console.log(firstColor); // Output: Red
console.log(secondColor); // Output: Green

// تخطي عناصر باستخدام فاصلة فارغة
const [, , thirdColor] = colors;
console.log(thirdColor); // Output: Blue

// قيم افتراضية
const [mainShade, secondaryShade, tertiaryShade = "Yellow"] = ["Orange", "Purple"];
console.log(tertiaryShade); // Output: Yellow (لأن العنصر الثالث غير موجود في المصفوفة الأصلية)
```

---

### 3. معامل الانتشار (Spread Syntax) `...`

معامل الانتشار يسمح بتوسيع تعبير قابل للتكرار (مثل مصفوفة أو سلسلة نصية) في الأماكن التي تتوقع فيها صفر أو أكثر من الوسائط ( لاستدعاءات الدوال) أو العناصر (للمصفوفات الحرفية).

**في المصفوفات:**

```javascript
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5]; // دمج عناصر arr1 مع عناصر جديدة
console.log(arr2); // Output: [1, 2, 3, 4, 5]

const str = "Hello";
const chars = [...str]; // تحويل السلسلة النصية إلى مصفوفة من الأحرف
console.log(chars); // Output: ['H', 'e', 'l', 'l', 'o']
```

**في الكائنات (ES2018+):**

```javascript
const obj1 = { a: 1, b: 2 };
const obj2 = { ...obj1, c: 3, b: 3 }; // الخاصية b في obj2 ستتجاوز الخاصية b من obj1 لأنها جاءت لاحقاً
console.log(obj2); // Output: { a: 1, b: 3, c: 3 }
```

**في استدعاء الدوال:**

```javascript
function sum(x, y, z) {
  return x + y + z;
}
const numbers = [1, 2, 3];
console.log(sum(...numbers)); // تمرير عناصر المصفوفة كوسائط منفصلة للدالة
// Output: 6
```

---

### 4. المعاملات المتبقية (Rest Parameters) `...`

صيغة المعاملات المتبقية تسمح لنا بتمثيل عدد غير محدد من الوسائط كـ مصفوفة. يجب أن يكون آخر معامل مُسمى في تعريف الدالة.

```javascript
// ...args تجمع كل الوسائط الممررة في مصفوفة اسمها args
function sumAll(...args) {
  let total = 0;
  for (const arg of args) {
    total += arg;
  }
  return total;
}

console.log(sumAll(1, 2, 3)); // Output: 6
console.log(sumAll(10, 20, 30, 40)); // Output: 100

// ...hobbies تجمع كل الوسائط بعد age في مصفوفة اسمها hobbies
function printUserInfo(name, age, ...hobbies) {
  console.log(`Name: ${name}, Age: ${age}`);
  console.log("Hobbies:", hobbies.join(", "));
}

printUserInfo("Sarah", 28, "Reading", "Traveling", "Coding");
// Output:
// Name: Sarah, Age: 28
// Hobbies: Reading, Traveling, Coding
```
**ملاحظة:** الفرق بين معامل الانتشار والمعاملات المتبقية يكمن في مكان استخدامهما. معامل الانتشار "يفرد" عناصر مصفوفة أو خصائص كائن، بينما المعاملات المتبقية "تجمع" الوسائط المتبقية في مصفوفة ضمن تعريف الدالة.

---

### 5. الأصناف (Classes)

الأصناف في جافاسكريبت هي "سكر syntactic sugar" فوق نظام الوراثة القائم على الـ prototype الموجود مسبقًا. تقدم صيغة أوضح وأبسط لإنشاء الكائنات والتعامل مع الوراثة.

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    // هذه الدالة خاصة بالصنف Animal
    console.log(`${this.name} makes a sound.`);
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name); // استدعاء constructor الخاص بالصنف الأب (Animal) لتمرير الاسم
    this.breed = breed;
  }

  speak() {
    // هذه الدالة تتجاوز (override) دالة speak الموجودة في الصنف Animal
    console.log(`${this.name} barks.`);
  }

  fetch() {
    // دالة خاصة بالصنف Dog
    console.log(`${this.name} fetches the ball.`);
  }
}

const myDog = new Dog("Rocky", "German Shepherd");
myDog.speak(); // Output: Rocky barks.
myDog.fetch(); // Output: Rocky fetches the ball.

const genericAnimal = new Animal("Creature");
genericAnimal.speak(); // Output: Creature makes a sound.
```

**الميزات الرئيسية للأصناف:**
* **`constructor`**: دالة خاصة لإنشاء وتهيئة الكائنات التي يتم إنشاؤها بواسطة الصنف.
* **`super`**: تستخدم لاستدعاء الدوال الموجودة في الصنف الأب (مثل `super()` لاستدعاء مُنشئ الأب أو `super.methodName()` لاستدعاء دالة من الأب).
* **`extends`**: تستخدم لإنشاء صنف فرعي يرث من صنف أب.
* **Getters و Setters**: دوال خاصة للتحكم في كيفية الوصول إلى خصائص الكائن وتعديلها.
* **Static Methods**: دوال تنتمي إلى الصنف نفسه وليس إلى экземпляرات (instances) الكائن، ويتم استدعاؤها مباشرة من الصنف (مثال: `ClassName.staticMethod()`).

---

### 6. الوحدات (Modules) - ES Modules

الوحدات تسمح بتقسيم الكود إلى ملفات منفصلة وقابلة لإعادة الاستخدام. ES Modules هي النظام القياسي للوحدات في جافاسكريبت الحديثة.

**تصدير (Exporting):**
يمكنك تصدير الدوال، الكائنات، أو القيم الأولية.

**ملف `math.js`:**
```javascript
// تصدير مُسمى (Named Export)
export const PI = 3.14159;

export function add(a, b) {
  return a + b;
}

export function subtract(a, b) {
  return a - b;
}

// تصدير افتراضي (Default Export) - يمكن أن يكون هناك واحد فقط لكل وحدة
const multiply = (a, b) => a * b;
export default multiply; // هذا هو التصدير الافتراضي للدالة multiply
```

**استيراد (Importing):**

**ملف `app.js` (يفترض أن يكون في نفس المجلد مع `math.js`):**
```javascript
// استيراد مُسمى، يمكن تغيير اسم الدالة المستوردة باستخدام as
import { PI, add as sumNumbers } from './math.js';

// استيراد كل ما هو مُسمى ووضعه في كائن واحد
import * as mathOperations from './math.js';

// استيراد التصدير الافتراضي، الاسم هنا (multiplyNumbers) اختياري ويمكن تغييره
import multiplyNumbers from './math.js';

console.log(PI); // Output: 3.14159
console.log(sumNumbers(5, 2)); // Output: 7

console.log(mathOperations.subtract(10, 4)); // Output: 6
// للوصول إلى التصدير الافتراضي من خلال الكائن *، نستخدم .default
console.log(mathOperations.default(3, 4)); // Output: 12

console.log(multiplyNumbers(3, 4)); // Output: 12
```

**ملاحظات هامة لاستخدام ES Modules في Node.js:**
* يجب حفظ الملفات بامتداد `.mjs` لكي يتعرف عليها Node.js كوحدات ES Modules بشكل افتراضي، أو
* يجب إضافة الحقل `"type": "module"` إلى ملف `package.json` الخاص بمشروعك. عندها يمكنك استخدام امتداد `.js` كالمعتاد.

---

بهذا نكون قد راجعنا أهم ميزات ES6+ التي ستحتاجها بكثرة. فهم هذه المفاهيم وتطبيقها بشكل جيد سيجعل رحلتك في تطوير الواجهات الخلفية أكثر سلاسة وفعالية.