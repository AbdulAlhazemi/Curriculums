
### ❓ اختبار (Quiz)

1.  **ما هو الإغلاق (Closure)؟**
    * A) دالة بدون اسم
    * B) طريقة لإنشاء ملفات
    * C) دالة تتذكر المتغيرات من النطاق الخارجي ✅
    * D) لا شيء مما سبق

2.  **ما ناتج الكود التالي؟**
    ```javascript
    function makeAdder(x) {
      return function(y) {
        return x + y;
      };
    }
    
    const add5 = makeAdder(5);
    console.log(add5(3));
    ```
    * A) 8 ✅
    * B) 53
    * C) undefined
    * D) خطأ

3.  **ما هو الهدف من currying؟**
    * A) كتابة حلقات أكثر كفاءة
    * B) تحسين تصميم الدوال ✅
    * C) التعامل مع قواعد البيانات
    * D) ضغط الكود

4.  **في الدوال السهمية، الكلمة `this` تشير إلى:**
    * A) الكائن الحالي
    * B) السياق الخارجي ✅
    * C) null
    * D) المتغير الأول

5.  **ماذا يحدث هنا؟**
    ```javascript
    const obj = {
      val: 100,
      arrow: () => console.log(this.val),
    };
    
    obj.arrow();
    ```
    * A) يطبع 100
    * B) يطبع undefined ✅
    * C) يطبع this
    * D) يعطي خطأ

---