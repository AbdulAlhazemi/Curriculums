### 🛠️ تمرين عملي
انظر إلى الدالة التالية. ما هي "روائح الكود" التي تكتشفها فيها؟ حاول إعادة هيكلتها لجعلها أنظف.

**الكود الأصلي:**
```javascript
function calculate(items) {
  let temp = 0;
  for (let i = 0; i < items.length; i++) {
    // Check if item is not expired
    if (items[i].exp > new Date()) {
      temp += items[i].p; // p is price
    }
  }
  return temp;
}
```

> **تلميح:** فكر في: الأسماء الغامضة (`calculate`, `items`, `temp`, `p`, `exp`)، وكيف يمكن جعل الشرط `if` أكثر وضوحًا.

---
