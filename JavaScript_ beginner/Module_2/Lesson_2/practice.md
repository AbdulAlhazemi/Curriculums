## 🧪 تحدي تدريبي: استخدام switch في JavaScript

### 🎯 التحدي:

في محرر JavaScript الخاص بك:

1. قم بالإعلان عن متغير باسم `day` يحتوي على اسم يوم مثل `"Monday"`، `"Tuesday"`، إلخ.  
2. استخدم جملة `switch` للتحقق من قيمة `day` واطبع التالي:
   - إذا كانت `"Monday"` → اطبع `"Start of the week"`
   - إذا كانت `"Wednesday"` → اطبع `"Midweek"`
   - إذا كانت `"Friday"` → اطبع `"Almost weekend"`
   - إذا كانت `"Saturday"` أو `"Sunday"` → اطبع `"Weekend!"`
   - استخدم `default` لطباعة `"Just another day"` لأي يوم آخر
3. تأكد من استخدام `break` بعد كل `case`.

---

### 💡 تلميحات:

- `switch` تُستخدم بدلاً من سلسلة طويلة من `if / else if`.
- استخدم `break` لمنع تنفيذ الحالات التالية بعد المطابقة.
- يمكن دمج أكثر من `case` لنفس الكود (مثال: `case "Saturday": case "Sunday":`).

---

### ✅ الحل النموذجي:

```javascript
let day = "Friday";

switch (day) {
  case "Monday":
    console.log("Start of the week");
    break;

  case "Wednesday":
    console.log("Midweek");
    break;

  case "Friday":
    console.log("Almost weekend");
    break;

  case "Saturday":
  case "Sunday":
    console.log("Weekend!");
    break;

  default:
    console.log("Just another day");
    break;
}
```