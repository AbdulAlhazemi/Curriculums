
### 🛠️ تمرين عملي (Practice)
🧩 **المطلوب:**
اكتب دالة `fetchUserData()` تحاكي جلب بيانات مستخدم باستخدام Promise، وانتظر النتيجة باستخدام async/await.

✍️ **ابدأ هنا:**
```javascript
function fetchUserData() {
  return new Promise(resolve => {
    setTimeout(() => resolve({ name: "Lina", age: 22 }), 1000);
  });
}

async function displayUser() {
  // كودك هنا
}

displayUser();
```
> 💡 **تلميح:** استخدم `await fetchUserData()` داخل الدالة `displayUser`.

---