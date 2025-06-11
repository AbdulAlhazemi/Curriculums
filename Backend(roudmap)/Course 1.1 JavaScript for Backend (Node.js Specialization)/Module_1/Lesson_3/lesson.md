## 🟩 الوحدة 1: جافاسكريبت الحديثة والمتقدمة (Advanced JS Foundations)

### 📘 الدرس 3: تنظيم الكود باستخدام Modularization

#### 🧠 **ماذا ستتعلم؟**
* ما هو modularization ولماذا هو مهم في تطبيقات الباكند.
* كيفية تقسيم الكود إلى وحدات قابلة لإعادة الاستخدام.
* الفرق بين CommonJS و ES Modules.
* أفضل الممارسات في تنظيم ملفات المشروع.

---

#### 1. ما المقصود بـ Modularization؟
هو أسلوب في كتابة الكود بحيث يتم **تقسيم المشروع إلى ملفات/وحدات مستقلة**، كل منها تحتوي على وظيفة أو منطق معين.

**🔧 لماذا؟**
* سهولة الصيانة والاختبار.
* إعادة استخدام الكود.
* تقليل التعقيد.

---

#### 2. مثال على كود غير منظم

```javascript
function calculatePrice(items) {
  // منطق طويل
}

function formatPrice(price) {
  // تنسيق السعر
}

// تابع للمستخدم
function createUser(name) {
  // ...
}
```
> 💥 **المشكلة:** كل شيء في ملف واحد = صعب الصيانة.

---

#### 3. تقسيم الكود إلى ملفات (Modules)

📄 **ملف: `priceUtils.js`**
```javascript
function calculatePrice(items) {
  return items.reduce((acc, item) => acc + item.price, 0);
}

function formatPrice(price) {
  return `$${price.toFixed(2)}`;
}

module.exports = { calculatePrice, formatPrice };
```

📄 **ملف: `userUtils.js`**
```javascript
function createUser(name) {
  return { name, id: Date.now() };
}

module.exports = { createUser };
```

📄 **ملف: `main.js`**
```javascript
const { calculatePrice, formatPrice } = require('./priceUtils');
const { createUser } = require('./userUtils');

const user = createUser('Ali');
const total = calculatePrice([{ price: 10 }, { price: 20 }]);
console.log(formatPrice(total));
```

---

#### 4. الفرق بين CommonJS و ES Modules

| التقنية | التصدير | الاستيراد | تستخدم في |
| :--- | :--- | :--- | :--- |
| **CommonJS** | `module.exports` | `require()` | Node.js (تقليديًا) |
| **ES Modules** | `export` | `import` | المتصفحات + Node (حديثًا) |

> 🔔 **ملاحظة:** إذا كنت تستخدم Node 14+ وتريد استخدام ES Modules، أضف `"type": "module"` في `package.json`.

---