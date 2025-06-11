## 🟩 الوحدة 1: جافاسكريبت الحديثة والمتقدمة (Advanced JS Foundations)

### 📘 الدرس 1: إتقان ميزات ES6+ في جافاسكريبت

#### 🧠 **ماذا ستتعلم؟**

* استخدام الدوال السهمية (Arrow Functions)
* استخراج القيم باستخدام التفكيك (Destructuring)
* استخدام معاملات النشر (Spread) والجمع (Rest)
* كتابة الكلاسات (Classes) في جافاسكريبت
* تنظيم الكود باستخدام الوحدات (Modules)

---

#### 1. الدوال السهمية (Arrow Functions)

الدوال السهمية هي طريقة مختصرة وأكثر وضوحًا لكتابة الدوال.

**دالة تقليدية:**
```javascript
function add(a, b) {
  return a + b;
}
```

**دالة سهمية:**
```javascript
const add = (a, b) => a + b;
```
> 🔎 **معلومة مهمة:** الدوال السهمية لا تملك `this` خاص بها — بل تأخذ القيمة من السياق الخارجي.

#### 2. التفكيك (Destructuring)

طريقة سهلة لاستخراج القيم من الكائنات والمصفوفات.

**تفكيك كائن:**
```javascript
const user = { name: "Ali", age: 25 };
const { name, age } = user;
```

**تفكيك مصفوفة:**
```javascript
const numbers = [1, 2, 3];
const [first, second] = numbers;
```

#### 3. Spread & Rest

✅ **Spread (لنشر القيم)**
```javascript
const arr1 = [1, 2];
const arr2 = [...arr1, 3, 4]; // [1, 2, 3, 4]
```

✅ **Rest (لجمع القيم)**
```javascript
function sum(...nums) {
  return nums.reduce((acc, curr) => acc + curr, 0);
}
```

#### 4. الكلاسات (Classes)

توفر طريقة منظمة لإنشاء كائنات ووراثة الخصائص.

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    return `Hello, I’m ${this.name}`;
  }
}

const p = new Person("Sara");
console.log(p.greet()); // Hello, I’m Sara
```

#### 5. الوحدات (Modules)

تساعد في تقسيم الكود إلى ملفات يمكن إعادة استخدامها.

**file1.js**
```javascript
export const PI = 3.14;
```

**file2.js**
```javascript
import { PI } from './file1.js';
console.log(PI);
```
