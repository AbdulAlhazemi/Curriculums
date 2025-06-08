🧪 **تحدي تدريبي**
1.	أنشئ متغيرًا `userTries` واضبط قيمته على `1`
2.	استخدم حلقة `do...while` لمحاكاة:
		"Attempting login…" حتى يصل `userTries` إلى 4
3.	اطبع "Attempt #1"، "Attempt #2"، إلخ.

تلميح:

```javascript
let userTries = 1;
do {
  console.log("Attempt #" + userTries);
  userTries++;
} while (userTries <= 3);
```
