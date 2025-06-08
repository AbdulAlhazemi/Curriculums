# الاختبار النهائي: أساسيات جافاسكريبت (مبتدئ)

## 📝 الجزء 1: تحدي البرمجة – مدير قائمة التسوق (25 نقطة)

**التعليمات:**
قم ببناء تطبيق صغير لإدارة قائمة التسوق باستخدام الكائنات والمصفوفات والدوال. أكمل كل خطوة في المحرر المدمج بالمتصفح.

**المتطلبات:**

1.  **إنشاء القائمة:**
    * أنشئ مصفوفة فارغة باسم `shoppingList`.

2.  **كائن المنتج:**
    * يجب أن يمثل كل عنصر في `shoppingList` كائنًا بالخصائص التالية:
        * `name` (string): اسم المنتج (مثل `"Milk"`)
        * `quantity` (number): الكمية (مثل `1`)
        * `purchased` (boolean): حالة الشراء (تبدأ بـ `false`)

3.  **دالة `addItem`:**
    * أنشئ دالة باسم `addItem` تأخذ `name` (اسم المنتج) و `quantity` (الكمية) كوسائط.
    * تقوم الدالة بإنشاء كائن منتج جديد (مع `purchased` بقيمة `false` افتراضيًا) وتضيفه إلى مصفوفة `shoppingList`.

4.  **دالة `markAsPurchased`:**
    * أنشئ دالة باسم `markAsPurchased` تأخذ `itemName` (اسم المنتج) كوسيط.
    * تبحث هذه الدالة عن المنتج في `shoppingList` بالاسم. إذا وجدته، تقوم بتغيير خاصية `purchased` الخاصة به إلى `true`.

5.  **دالة `displayList`:**
    * أنشئ دالة باسم `displayList` تقوم بطباعة القائمة بأكملها.
    * لكل عنصر، اطبع حالته (تم شراؤه أم لا)، اسمه، وكميته. مثال:
        * `"[ ] Milk (Quantity: 1)"` (إذا لم يتم شراؤه)
        * `"[x] Bread (Quantity: 2)"` (إذا تم شراؤه)
    * استخدم حلقة `for...of` للمرور على `shoppingList`.

6.  **دالة `getPendingItemsSummary`:**
    * أنشئ دالة باسم `getPendingItemsSummary`.
    * يجب أن تُرجع هذه الدالة سلسلة نصية تلخص عدد العناصر التي لم يتم شراؤها بعد. مثال: `"You have 3 items left to buy."`

**مثال على الاستخدام (لا تكتب هذا في حلك، فقط للاسترشاد):**

```javascript
// addItem("Milk", 1);
// addItem("Bread", 2);
// addItem("Apples", 5);
// markAsPurchased("Bread");
// displayList();
// console.log(getPendingItemsSummary());

/* الناتج المتوقع من المثال أعلاه:
[ ] Milk (Quantity: 1)
[x] Bread (Quantity: 2)
[ ] Apples (Quantity: 5)
You have 2 items left to buy.
*/
```

---

## 🧩 الجزء 2: مقتطفات برمجية (30 نقطة - 3 نقاط لكل سؤال)

أكمل كل مهمة أو أجب عن السؤال بكتابة الكود المطلوب:

1.  **إنشاء متغير:** قم بالإعلان عن متغير `city` باستخدام `const` وأسند إليه قيمة اسم مدينتك كسلسلة نصية.
2.  **التحويل إلى رقم:** قم بتحويل السلسلة النصية `"101"` إلى رقم وخزنها في متغير `numericValue`.
3.  **المعامل الثلاثي:** اكتب تعبيرًا ثلاثيًا يتحقق إذا كان المتغير `temperature` (افترض أنه موجود) أكبر من `25`. إذا كان كذلك، يجب أن تكون النتيجة `"Hot"`; وإلا، `"Cool"`. أسند النتيجة إلى متغير `weatherCondition`.
4.  **تعبير دالة:** اكتب تعبير دالة (function expression) مخزن في متغير `calculateSum` يأخذ معاملين `a` و `b` ويُرجع مجموعهما.
5.  **الوصول للمصفوفة:** لديك مصفوفة `let letters = ["a", "b", "c", "d"];`. اكتب الكود للوصول إلى العنصر `"c"`.
6.  **`push` و `pop`:** لديك مصفوفة `let numbers = [10, 20];`. أضف `30` إلى نهايتها، ثم قم بإزالة العنصر الأخير. ما هي قيمة `numbers` الآن؟ (اكتب الكود الذي يؤدي لذلك والناتج المتوقع كتعليق).
7.  **خصائص الكائن:** أنشئ كائنًا `book` بخاصية `title` وقيمتها `"The Great Gatsby"` وخاصية `year` بقيمتها `1925`.
8.  **تعديل خاصية:** للكائن `book` من السؤال السابق، قم بتحديث خاصية `year` إلى `1926`.
9.  **حلقة `for...of`:** لديك مصفوفة `let data = [1, 2, 3];`. اكتب حلقة `for...of` تطبع كل عنصر.
10. **حلقة `for...in`:** لديك كائن `let car = { make: "Toyota", model: "Camry" };`. اكتب حلقة `for...in` تطبع كل مفتاح وقيمة بالصيغة `key: value`.

---

## 🐞 الجزء 3: تصحيح الأخطاء (20 نقطة - 4 نقاط لكل سؤال)

ابحث عن الخطأ في كل مقتطف كود وقم بإصلاحه. اشرح الخطأ بإيجاز في تعليق.

1.  ```javascript
    for (let i = 0; i < 5; i) {
      console.log(i); // أريد طباعة الأرقام من 0 إلى 4
    }
    ```
2.  ```javascript
    let user = {
      name: "Sara"
      age: 28 // خطأ هنا
    };
    console.log(user.name);
    ```
3.  ```javascript
    function checkValue(value) {
      if (value = 10) { // خطأ منطقي هنا
        return "Value is 10";
      } else {
        return "Value is not 10";
      }
    }
    console.log(checkValue(5));
    ```
4.  ```javascript
    showMessage(); // محاولة استدعاء قبل التعريف
    const showMessage = function() {
      console.log("This is a message.");
    };
    ```
5.  ```javascript
    let count = 5;
    do {
      console.log(count);
      // لا يوجد تحديث للمتغير count
    } while (count > 0);
    ```

---

## 📋 الجزء 4: اختبار المفاهيم (اختيار من متعدد – 15 نقطة - 1.5 نقطة لكل سؤال)

اختر الإجابة الصحيحة.

1.  ما هو الناتج الرئيسي لدالة لا تحتوي على جملة `return` صريحة؟
    
    أ) `null`
    
    ب) `0`
    
    ج) `undefined` ✅
    
    د) يسبب خطأ

2.  أي من التالي يُستخدم للإعلان عن متغير لا يمكن إعادة إسناد قيمة جديدة له؟

    أ) `var`

    ب) `let`

    ج) `const` ✅
    
    د) `static`

3.  ماذا يطبع الكود التالي؟

    ```javascript
    console.log("5" + 5);
    ```

    أ) `10`
    
    ب) `"55"` ✅
    
    ج) `NaN`
    
    د) خطأ

4.  في حلقة `for (let i = 0; i < 3; i++)`, أي جزء هو `i++`؟

    أ) التهيئة (Initialization)

    ب) الشرط (Condition)

    ج) التحديث (Update) ✅

    د) جسم الحلقة (Loop body)

5.  أي دالة مصفوفة تُستخدم لإزالة العنصر الأخير من مصفوفة وتُرجع ذلك العنصر؟

    أ) `.shift()`

    ب) `.unshift()`

    ج) `.push()`

    د) `.pop()` ✅

6.  كيف تصل إلى خاصية `model` في كائن `car` إذا كان اسم الخاصية مخزناً في متغير `propName`؟

    أ) `car.propName`

    ب) `car[propName]` ✅

    ج) `car(propName)`

    د) `car{propName}`

7.  ما هي الكلمة المفتاحية التي تستخدم للخروج الفوري من حلقة تكرار؟

    أ) `continue`

    ب) `return`

    ج) `break` ✅

    د) `exit`

8.  ماذا تعني "IIFE"؟

    أ) Internal Interface For Execution

    ب) Immediately Invoked Function Expression ✅

    ج) Initial Input Function Element

    د) Inherited Invocation For ECMAScript

9.  ماذا يُرجع `typeof null` في جافاسكريبت؟

    أ) `"null"`

    ب) `"undefined"`

    ج) `"object"` ✅

    د) `"none"`

10. أي من المعاملات التالية يقوم بمقارنة صارمة (strict equality)؟

    أ) `==`

    ب) `=`

    ج) `===` ✅

    د) `!=`

---