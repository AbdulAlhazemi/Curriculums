## 🧱 الوحدة 1: مدخل إلى التفكير الخوارزمي

### 📘 الدرس 6: الصفوف (Queues)

#### 🧠 **ماذا ستتعلم؟**
* ما هو الصف (Queue)؟
* مبدأ “FIFO” (First-In, First-Out).
* العمليات الأساسية: `enqueue`, `dequeue`, `peek`.
* كيفية تنفيذ صف باستخدام JavaScript.
* أمثلة واقعية على استخدام الصفوف.

---
### 🧾 1. ما هو الصف؟
الصف هو بنية بيانات خطية تتبع مبدأ **“أول من يدخل، هو أول من يخرج” (First-In, First-Out - FIFO)**.

يمكنك تخيله مثل طابور انتظار في بنك أو متجر:
* الشخص الذي يدخل الطابور أولًا هو من يُخدم أولًا.
* أي شخص جديد ينضم إلى **نهاية** الطابور.

---
### 🧾 2. العمليات الأساسية
| العملية | الوصف | التعقيد الزمني (عند استخدام مصفوفة) |
| :--- | :--- | :--- |
| `enqueue` | إضافة عنصر إلى **نهاية** الصف. | $O(1)$ |
| `dequeue` | إزالة العنصر من **بداية** الصف. | $O(n)$ |
| `peek` | عرض العنصر **الأول** دون إزالته. | $O(1)$ |
| `isEmpty`| التحقق إذا ما كان الصف فارغًا. | $O(1)$ |

> **ملاحظة:** استخدام `shift()` لحذف العنصر الأول في مصفوفة يجعل تعقيد `dequeue` هو $O(n)$. يمكن تحقيق $O(1)$ باستخدام هياكل بيانات أخرى مثل القوائم المرتبطة.

---
### 🧾 3. تنفيذ Queue باستخدام JavaScript
أبسط طريقة لتنفيذ الصف هي باستخدام مصفوفة.

```javascript
class Queue {
  constructor() {
    this.items = [];
  }

  // إضافة عنصر إلى نهاية الصف
  enqueue(element) {
    this.items.push(element);
  }

  // إزالة عنصر من بداية الصف
  dequeue() {
    if (this.isEmpty()) {
      return "Underflow"; // لا يمكن الحذف من صف فارغ
    }
    return this.items.shift();
  }

  // إلقاء نظرة على العنصر في بداية الصف
  peek() {
    if (this.isEmpty()) {
      return "No items in Queue";
    }
    return this.items[0];
  }

  // التحقق من أن الصف فارغ
  isEmpty() {
    return this.items.length === 0;
  }

  // طباعة عناصر الصف
  print() {
    console.log(this.items.join(" <- "));
  }
}
```

---
### 🧾 4. مثال عملي
```javascript
const queue = new Queue();

queue.enqueue("Ahmed");
queue.enqueue("Sara");
queue.enqueue("Lina");

queue.print(); // "Ahmed <- Sara <- Lina"

console.log(queue.dequeue()); // "Ahmed"
console.log(queue.peek());    // "Sara"
```

---
