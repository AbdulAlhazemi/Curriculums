# الوحدة 4: المصفوفات والكائنات

## اختبار الوحدة 4: المصفوفات والكائنات

بالطبع! إليك الجزء 1 من التحدي البرمجي مكتوبًا بتنسيق Markdown مع التلميح مضافًا في قسم خاص:

## 📝 الجزء 1: تحدي البرمجة – تطبيق قائمة جهات الاتصال

**التعليمات:**  
قم ببناء قائمة جهات اتصال صغيرة باستخدام الكائنات والمصفوفات. أكمل كل خطوة في المحرر المدمج بالمتصفح.

### 💼 المتطلبات:

- أنشئ **مصفوفة فارغة** باسم `contacts`.
- أضف **3 كائنات** جهات اتصال، كل منها يحتوي على:
  - `name` (سلسلة نصية)
  - `email` (سلسلة نصية)
  - `phone` (سلسلة نصية)
- أنشئ دالة `addContact` تأخذ كائن جهة اتصال وتضيفه إلى القائمة.
- أنشئ دالة `listContacts` تقوم بطباعة **اسم ورقم هاتف** كل جهة اتصال.
- أضف دالة (method) لكل جهة اتصال تسمى `greet` تطبع رسالة مخصصة مثل:  
  `"Hi, I’m [name]. You can reach me at [email]."`

### 💡 مثال على الناتج:

Hi, I’m Alex. You can reach me at alex@example.com.
Hi, I’m Jamie. You can reach me at jamie@example.com.
Hi, I’m Taylor. You can reach me at taylor@example.com.

---

### 🧠 تلميح:

- يمكنك إنشاء كائن جهة اتصال بهذا الشكل:

```javascript
let contact = {
  name: "Alex",
  email: "alex@example.com",
  phone: "123-456-7890",
  greet: function() {
    console.log(`Hi, I'm ${this.name}. You can reach me at ${this.email}.`);
  }
};
```

	•	لا تنسَ استخدام contacts.push(contact) داخل دالة addContact.
	•	استخدم حلقة for...of في listContacts للطباعة.


## 🧩 الجزء 2: التعامل مع المصفوفات والكائنات (10 تمارين)

**التعليمات:**  
أكمل كل مهمة برمجية حسب القائمة التالية:

### ✅ المهام:

1. أنشئ **مصفوفة** باسم `fruits` تحتوي على `"apple"`، `"banana"`، و `"cherry"`.
2. أضف `"orange"` إلى **نهاية** مصفوفة `fruits`.
3. قم **بإزالة** الفاكهة الأولى من المصفوفة.
4. استخدم `slice()` للحصول على **آخر فاكهتين** من `fruits`.
5. أنشئ **كائنًا** باسم `movie` يحتوي على:
   - `title` (العنوان)
   - `year` (السنة)
   - `rating` (التقييم)
6. قم **بتحديث** `rating` إلى `9.5`.
7. أضف مفتاحًا جديدًا `genre` بقيمة `"action"`.
8. **احذف** خاصية `year` من الكائن.
9. استخدم حلقة `for...in` لطباعة جميع **مفاتيح وقيم** الكائن.
10. أضف دالة (method) إلى `movie` باسم `describe` تطبع:  
    `"Title: [title], Genre: [genre], Rating: [rating]"`

---

### 💡 تلميح:

- يمكنك استخدام الدوال التالية:
  - `push()` لإضافة عنصر إلى نهاية المصفوفة
  - `shift()` لإزالة أول عنصر من المصفوفة
  - `slice(start)` أو `slice(start, end)` للحصول على جزء من المصفوفة
- للوصول إلى قيم الكائن استخدم:  
  `movie.title` أو `movie["title"]`
- لإضافة خاصية جديدة:  
  `movie.genre = "action"`
- لحذف خاصية:  
  `delete movie.year`
- لصنع method داخل الكائن:  
```javascript
describe: function() {
  console.log(`Title: ${this.title}, Genre: ${this.genre}, Rating: ${this.rating}`);
}
---



📋 **الجزء 3: اختبار المفاهيم (اختيار من متعدد – 10 أسئلة)**

اختر الإجابة الصحيحة.
1.  على ماذا تتكرر حلقة `for...of`؟

    أ) مفاتيح الكائن

    ب) قيم المصفوفة ✅

    ج) أسماء الخصائص

    د) أسماء الدوال

2.  أي دالة تضيف عنصرًا إلى نهاية المصفوفة؟

    أ) `push()` ✅

    ب) `pop()`

    ج) `shift()`

    د) `unshift()`

3.  كيف تصل إلى قيمة `email` من هذا الكائن؟

    ```javascript
    let user = { email: "user@example.com" };
    ```

    أ) `user[email]`

    ب) `user."email"`

    ج) `user.email` ✅

    د) `email.user`


---