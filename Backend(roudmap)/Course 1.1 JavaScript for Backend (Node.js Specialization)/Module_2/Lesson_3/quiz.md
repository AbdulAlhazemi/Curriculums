### ❓ اختبار (Quiz)
1.  **ما هي قيمة `this` في الدالة التالية داخل المتصفح؟**
    ```javascript
    function test() {
      console.log(this);
    }
    test();
    ```
    * A) الكائن global في Node
    * B) undefined
    * C) window ✅
    * D) null

2.  **ماذا تُعيد `arrow function` عندما تستخدم `this`؟**
    * A) دائمًا `window`
    * B) تأخذ `this` من السياق المحيط ✅
    * C) تشير للكائن الحالي
    * D) undefined دائمًا

3.  **ما الفرق بين `call()` و `bind()`؟**
    * A) لا يوجد فرق
    * B) `call()` يعيد دالة جديدة
    * C) `bind()` يعيد دالة جديدة دون تنفيذها ✅
    * D) `bind()` ينفذ الدالة مباشرة

4.  **في أي حالة تكون قيمة `this` هي `undefined`؟**
    * A) في الكائنات
    * B) داخل الدوال في الوضع الصارم ✅
    * C) دائمًا في `setTimeout`
    * D) في `arrow functions`

5.  **ما ناتج الكود التالي؟**
    ```javascript
    const user = {
      name: "Mona",
      greet: function () {
        console.log(this.name);
      }
    };

    const g = user.greet;
    g(); // ؟
    ```
    * A) “Mona”
    * B) undefined ✅
    * C) خطأ
    * D) null

***