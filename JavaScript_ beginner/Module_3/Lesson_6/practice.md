🧪 **تحدي تدريبي**
1.	اكتب IIFE تقوم بطباعة "JS is fun!"
2.	أنشئ IIFE تأخذ رقمًا وتطبع مربعه.
3.	حاول الإعلان عن متغير داخل IIFE وقم بطباعته في الخارج—ماذا يحدث؟

تلميح:
```javascript
(function() {
  console.log("JS is fun!");
})();

(function(num) {
  console.log("Square:", num * num);
})(5);
```
