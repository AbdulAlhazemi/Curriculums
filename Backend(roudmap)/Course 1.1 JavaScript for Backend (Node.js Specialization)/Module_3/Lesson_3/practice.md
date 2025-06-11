### 🛠️ تمرين عملي (Practice)

🧩 **المطلوب:**
1.  أنشئ ملفًا `log.txt` (يمكنك إنشاؤه يدويًا أو باستخدام `fs.writeFileSync`).
2.  اكتب كودًا يقرأ هذا الملف باستخدام `fs`.
3.  ثم يطبع المسار الكامل باستخدام `path`.

✍️ **نموذج:**
```javascript
const fs = require('fs');
const path = require('path');

// Step 1: Create the file
fs.writeFileSync('log.txt', 'This is a log file.');

// Step 2 & 3: Read the file and log its path
const filePath = path.join(__dirname, 'log.txt');

fs.readFile(filePath, 'utf8', (err, data) => {
  if (err) {
      console.error("Error reading the file:", err);
      return;
  }
  console.log("المحتوى:", data);
  console.log("المسار الكامل:", filePath);
});
```
> 💡 **تلميح:** جرب تعديل اسم الملف في `readFile` إلى اسم غير موجود لرؤية الخطأ الناتج.

***
