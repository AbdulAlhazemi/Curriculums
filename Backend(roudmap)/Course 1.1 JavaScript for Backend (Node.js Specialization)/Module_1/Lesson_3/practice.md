### 🛠️ تمرين عملي (Practice)

🧩 **المطلوب:**
1.  أنشئ ملفين:
    * `mathUtils.js`: يحتوي دالتين `add(a, b)` و `subtract(a, b)`.
    * `main.js`: يستورد الدوال ويجربها.

✍️ **نموذج البداية - `mathUtils.js`**
```javascript
function add(a, b) {
  return a + b;
}

function subtract(a, b) {
  return a - b;
}

module.exports = { add, subtract };
```

✍️ **`main.js`**
```javascript
const { add, subtract } = require('./mathUtils');
console.log(add(5, 3)); // 8
console.log(subtract(10, 4)); // 6
```
> 💡 **تلميح:** جرب تشغيل `node main.js` في المحرر لمعرفة النتيجة.

---
