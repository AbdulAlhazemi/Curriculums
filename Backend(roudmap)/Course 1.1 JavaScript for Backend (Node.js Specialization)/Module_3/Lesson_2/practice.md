### 🛠️ تمرين عملي (Practice)

🧩 **المطلوب:**
* اكتب كودًا يستخدم `setTimeout()` و `fs.readFile()` داخل نفس الملف.
* لاحظ ترتيب الإخراج في الطرفية، لتفهم أولوية التنفيذ.

✍️ **نموذج:**
```javascript
const fs = require('fs');

console.log("أ");

setTimeout(() => {
  console.log("ب");
}, 0);

// Create a dummy file.txt for the example to work
fs.writeFileSync('file.txt', 'hello'); 

fs.readFile("file.txt", "utf8", () => {
  console.log("ج");
});

console.log("د");
```
> 💡 **تلميح:** لاحظ أن `fs.readFile` قد يتم قبل أو بعد `setTimeout` حسب سرعة النظام.

***