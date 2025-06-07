🧪 **تحدي تدريبي**
1.	حاول استدعاء دالة مُعرفة باستخدام `function` قبل تعريفها.
2.	حاول استدعاء دالة مخزنة في `const` قبل تعريفها.
3.	حاول طباعة متغير `var`، `let`، و `const` قبل الإعلان عنهم.

تلميح:
```javascript
sayHi(); // يعمل

function sayHi() {
  console.log("Hi!");
}

sayBye(); // خطأ

const sayBye = function() {
  console.log("Bye!");
};

console.log(a); // الناتج: undefined
var a = 10;

console.log(b); // خطأ
let b = 20;
```