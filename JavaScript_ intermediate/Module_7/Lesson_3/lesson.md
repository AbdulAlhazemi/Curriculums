# الوحدة 7: أنماط كتابة الكود المتقدمة
**(Advanced Code Patterns)**

## الدرس 3: جحيم الاستدعاءات (Callback Hell) مقابل Promises و Async/Await

🧠 **ماذا ستتعلم**
* ما هو جحيم الاستدعاءات ولماذا يحدث.
* كيفية التعامل مع الكود غير المتزامن باستخدام الـ Callbacks.
* مقدمة إلى الـ Promises وكيف تحل مشاكل الـ Callbacks.
* استخدام Async/Await لكتابة كود غير متزامن أكثر وضوحًا.

***

### 🧾 1. ما هو جحيم الاستدعاءات؟
**جحيم الاستدعاءات (Callback Hell)** هو مصطلح لوصف الكود الذي يحتوي على **تداخل متكرر** في استدعاءات الدوال غير المتزامنة (Callbacks)، مما يجعل الكود صعب القراءة والصيانة.

***

### 🧠 مثال على جحيم الاستدعاءات:
```javascript
doSomething(function(result) {
  doSomethingElse(result, function(newResult) {
    doThirdThing(newResult, function(finalResult) {
      console.log('النتيجة النهائية:', finalResult);
    });
  });
});
```
هذا الشكل من الكود يسمى أحيانًا **“هرم الموت”** بسبب التداخل العميق.

***

### 📚 2. حل المشكلة باستخدام Promises
الـ **Promise** هو كائن يمثل نتيجة عملية غير متزامنة مستقبلية.

**مثال:**
```javascript
doSomething()
  .then(result => doSomethingElse(result))
  .then(newResult => doThirdThing(newResult))
  .then(finalResult => {
    console.log('النتيجة النهائية:', finalResult);
  })
  .catch(error => {
    console.error('حدث خطأ:', error);
  });
```
هنا، الكود أصبح أكثر وضوحًا وسهولة في القراءة.

***

### 🔧 3. استخدام Async/Await
**Async/Await** هي طريقة حديثة لبناء الكود غير المتزامن تشبه الكود المتزامن، مما يجعل القراءة أسهل.

```javascript
async function main() {
  try {
    const result = await doSomething();
    const newResult = await doSomethingElse(result);
    const finalResult = await doThirdThing(newResult);
    console.log('النتيجة النهائية:', finalResult);
  } catch (error) {
    console.error('حدث خطأ:', error);
  }
}

main();
```

***

### ⚠️ 4. ملاحظات
* لا تستخدم Callbacks إلا إذا كنت بحاجة لذلك أو في حالات محددة.
* استخدم **Promises** و **Async/Await** لكتابة كود نظيف وسهل الصيانة.

***

### 🚀 ماذا بعد؟
في الدرس القادم سنتحدث عن **تنظيم الكود باستخدام الوحدات (Modularization)** وكيفية استخدام `import` و `export` لتقسيم الكود.

***
