# الوحدة 3: الدوال (Functions)

## الدرس 2: المعاملات (Parameters) والوسائط (Arguments)

🧠 **ماذا ستتعلم**
*	ما هي معاملات الدوال ووسائطها
*	كيفية تمرير البيانات إلى الدالة
*	كيفية استخدام معاملات متعددة
*	ماذا يحدث عند تمرير عدد كبير جدًا أو قليل جدًا من الوسائط

---

📥 **1. ما هي المعاملات (Parameters) والوسائط (Arguments)؟**
*	**المعاملات (Parameters)** هي بمثابة عناصر نائبة—أسماء مدرجة في تعريف الدالة.
*	**الوسائط (Arguments)** هي القيم الفعلية التي تمررها عند استدعاء الدالة.

مثال:
```javascript
function greet(name) {  // 'name' هو معامل (parameter)
  console.log("Hello, " + name + "!");
}

greet("Alice");         // "Alice" هي وسيط (argument)
```

الناتج:
```
Hello, Alice!
```

---

➕ **2. معاملات متعددة**

يمكنك إضافة أكثر من معامل واحد عن طريق فصلهم بفواصل:
```javascript
function add(a, b) {
  console.log(a + b);
}

add(3, 4); // الناتج: 7
//`a` و `b` معاملان.
// ٤ و ٣ هما وسيطان يتم تمريرهما عند استدعاء الدالة
```


---

🧪 **3. جرب بنفسك**
```javascript
function introduce(firstName, age) {
  console.log("My name is " + firstName + " and I'm " + age + " years old.");
}

introduce("Liam", 21);
```

---

❓ **4. ماذا لو مررت عددًا خاطئًا من الوسائط؟**

جافاسكريبت لن تُظهر خطأ. بدلاً من ذلك:
*	**عدد قليل جدًا من الوسائط:** المعاملات المفقودة تكون `undefined`.

    ```javascript
    function sayName(name, title) {
      console.log(title + " " + name);
    }

    sayName("Jordan"); // الناتج: undefined Jordan
    ```
    
*	**عدد كبير جدًا من الوسائط:** يتم تجاهل القيم الإضافية.
    ```javascript
    function greet(name) {
      console.log("Hi " + name);
    }

    greet("Sam", "Smith"); // الناتج: Hi Sam
    ```

---

⚙️ **5. المعاملات الافتراضية (إضافة)**

يمكنك إعطاء المعاملات قيمة افتراضية في حال لم يتم تمرير وسيط.
```javascript
function greet(name = "friend") {
  console.log("Hi " + name);
}

greet();      // الناتج: Hi friend
greet("Ella");  // الناتج: Hi Ella
```

---

🧠 **النقاط الرئيسية**
*	المعاملات هي متغيرات في تعريفات الدوال.
*	الوسائط هي القيم الفعلية التي يتم تمريرها أثناء استدعاءات الدوال.
*	يمكنك استخدام معاملات متعددة.
*	استخدم القيم الافتراضية لجعل الدوال أكثر أمانًا.

---