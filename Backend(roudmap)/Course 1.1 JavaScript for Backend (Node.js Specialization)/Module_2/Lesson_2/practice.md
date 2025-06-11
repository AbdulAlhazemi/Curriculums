### 🛠️ تمرين عملي (Practice)

🧩 **المطلوب:**
* اكتب كودًا يحتوي على `setTimeout` و `console.log` قبل وبعده.
* لاحظ ترتيب الطباعة لفهم عمل Event Loop.

✍️ **نموذج:**

```javascript
console.log("قبل");
setTimeout(() => {
  console.log("داخل setTimeout");
}, 1000);
console.log("بعد");
```
> 💡 **تلميح:** لا تعتمد على “المدة الزمنية” فقط، بل على تفريغ Call Stack أولًا.
