🧪 **تحدي تدريبي**
1.	أنشئ مصفوفة `cities` تحتوي على 3 أسماء مدن على الأقل.
2.	قم بالمرور عليها باستخدام `for...of` واطبع كل مدينة.
3.	أنشئ كائنًا `employee` يحتوي على `name` (الاسم)، `position` (المنصب)، و `salary` (الراتب).
4.	استخدم `for...in` لطباعة كل مفتاح وقيمة من الكائن.

تلميح:
```javascript
let cities = ["Paris", "Tokyo", "Cairo"];
for (let city of cities) {
  console.log(city);
}

let employee = {
  name: "Jordan",
  position: "Developer",
  salary: 75000
};

for (let key in employee) {
  console.log(`${key}: ${employee[key]}`);
}
```
