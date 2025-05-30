# الوحدة 2: التحكم في التدفق

## الدرس 4: حلقات `while` و `do...while`

🧠 **ماذا ستتعلم**
*	كيف تعمل حلقات `while` و `do...while`
*	الفرق بينهما
*	متى تستخدم كل نوع من الحلقات
*	كيفية تجنب الحلقات اللانهائية

---

🔁 **1. ما هي الحلقة (Loop)؟**

الحلقات تسمح لك بتكرار الكود طالما كان الشرط صحيحًا (`true`).
بدلاً من كتابة نفس السطر مرارًا وتكرارًا، تخبر البرنامج أن يقوم بذلك تلقائيًا.

---

➿ **2. حلقة `while`**

تعمل حلقة `while` طالما كان الشرط صحيحًا (`true`).

البنية (Syntax):
```javascript
while (condition) {
  // الكود المراد تكراره
}
```

مثال:
```javascript
let count = 1;

while (count <= 5) {
  console.log("Count is:", count);
  count++;
}
```

هذا يطبع:
```
Count is: 1
Count is: 2
Count is: 3
Count is: 4
Count is: 5
```

كيف تعمل:
*	تتحقق من الشرط `count <= 5`
*	تنفذ كتلة الكود إذا كان الشرط `true`
*	تزيد قيمة `count`
*	تكرر حتى يصبح الشرط `false`

---

🔂 **3. حلقة `do...while`**

تعمل حلقة `do...while` دائمًا مرة واحدة على الأقل، حتى لو كان الشرط خاطئًا (`false`).

البنية (Syntax):
```javascript
do {
  // الكود المراد تنفيذه
} while (condition);
```

مثال:
```javascript
let number = 1;

do {
  console.log("Number is:", number);
  number++;
} while (number <= 3);
```

حتى لو بدأ الشرط خاطئًا (`false`)، يتم تنفيذ الكود مرة واحدة.
```javascript
let x = 10;

do {
  console.log("Hello");
} while (x < 5); // ما زال يطبع "Hello" مرة واحدة!
```

---

⚠️ **4. احترس من الحلقات اللانهائية**

يجب أن تتوقف الحلقة في النهاية. إذا لم يصبح الشرط خاطئًا (`false`) أبدًا، فستحصل على حلقة لا نهائية.

🚫 **سيء:**
```javascript
while (true) {
  console.log("This never ends!");
}
```

✅ **جيد:**
```javascript
let i = 0;
while (i < 3) {
  console.log(i);
  i++;
}
```

تأكد دائمًا:
*	أن شرط الحلقة سيصبح `false` في النهاية
*	أنك تقوم بتحديث متغيراتك بشكل صحيح (مثل `i++`)

---

🧪 **جرب بنفسك**

انسخ هذا وشغله في المحرر الخاص بك:
```javascript
let countdown = 5;

while (countdown > 0) {
  console.log(countdown);
  countdown--;
}
```
الآن حاول تحويلها إلى حلقة `do...while` ولاحظ التغييرات.

---

🧠 **النقاط الرئيسية**
*	استخدم `while` عندما يجب التحقق من الشرط قبل بدء الحلقة.
*	استخدم `do...while` عندما تحتاج إلى تشغيل الحلقة مرة واحدة على الأقل.
*	قم دائمًا بتحديث متغيرات الحلقة لمنع الحلقات اللانهائية.



---

🧪 **تحدي تدريبي**
1.	أنشئ متغيرًا `userTries` واضبط قيمته على `1`
2.	استخدم حلقة `do...while` لمحاكاة:
	*	"Attempting login…" حتى يصل `userTries` إلى 4
3.	اطبع "Attempt #1"، "Attempt #2"، إلخ.

تلميح:

```javascript
let userTries = 1;
do {
  console.log("Attempt #" + userTries);
  userTries++;
} while (userTries <= 3);
```

---