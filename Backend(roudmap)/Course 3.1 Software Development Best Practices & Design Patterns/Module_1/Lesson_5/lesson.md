## 📐 الوحدة 1: مبادئ الكود النظيف وأنماط التصميم

### 📘 الدرس 5: الأنماط الإنشائية الشائعة (Common Creational Patterns)

#### 🧠 **ماذا ستتعلم**
* ما هي الأنماط الإنشائية وما هو الغرض منها.
* كيفية عمل نمط Singleton ومتى نستخدمه.
* كيفية عمل نمط Factory Method وفوائده.
* تطبيق كلا النمطين باستخدام أمثلة عملية في جافاسكريبت.

---
### 🤔 1. ما هي الأنماط الإنشائية؟
الأنماط الإنشائية (Creational Patterns) هي أنماط تصميم توفر طرقًا مرنة **لإنشاء الكائنات (Objects)**. بدلاً من إنشاء الكائنات مباشرة باستخدام `new Object()`، تمنحك هذه الأنماط تحكمًا أكبر في عملية الإنشاء، مما يجعل نظامك أكثر مرونة وقابلية لإعادة الاستخدام.

---
### ☝️ 2. نمط Singleton
**الهدف:** ضمان أن يكون للكلاس **نسخة واحدة فقط (single instance)**، وتوفير نقطة وصول عامة (global) لهذه النسخة.

* **المشكلة التي يحلها:** أحيانًا، تحتاج إلى كائن واحد فقط لإدارة مورد مشترك في تطبيقك بالكامل. أمثلة:
    * كائن الاتصال بقاعدة البيانات.
    * كائن لإدارة الإعدادات العامة للتطبيق.
    * كائن لتسجيل الأحداث (Logger).
    إنشاء نسخ متعددة من هذه الكائنات قد يسبب تضاربًا أو يهدر الموارد.

* **التطبيق في JavaScript:**
    أسهل طريقة لتطبيق نمط Singleton في بيئة Node.js هي عن طريق الاستفادة من كيفية عمل الوحدات (Modules). عندما تقوم باستيراد وحدة، يقوم Node.js بإنشائها وتخزينها مؤقتًا. أي استيراد لاحق لنفس الوحدة سيُرجع نفس النسخة المخزنة.

    **مثال: `databaseConnection.js`**
    ```javascript
    class DatabaseConnection {
      constructor() {
        // منطق الاتصال بقاعدة البيانات يحدث هنا مرة واحدة فقط
        console.log('Creating a new database connection...');
        this.createdAt = new Date();
      }
      // ... دوال أخرى
    }

    // نقوم بإنشاء النسخة الوحيدة هنا
    const instance = new DatabaseConnection();

    // نقوم بتصدير هذه النسخة فقط
    module.exports = instance;
    ```
    **الاستخدام في ملف آخر:**
    ```javascript
    const dbInstance1 = require('./databaseConnection.js');
    const dbInstance2 = require('./databaseConnection.js');

    // سيطبع 'true' لأن كلاهما يشير إلى نفس النسخة
    console.log(dbInstance1 === dbInstance2); 
    ```

---
### 🏭 3. نمط Factory Method
**الهدف:** توفير واجهة لإنشاء الكائنات، مع ترك القرار للكلاسات الفرعية بتحديد أي كلاس سيتم إنشاؤه.

* **المشكلة التي يحلها:** تخيل أن لديك نظامًا يحتاج إلى إنشاء أنواع مختلفة من الكائنات التي تشترك في واجهة مشتركة (مثل إنشاء أنواع مختلفة من الإشعارات: `Email`, `SMS`, `Push`). بدلاً من وضع منطق `if/else` أو `switch` في كل مكان لإنشاء النوع الصحيح، يمكنك تفويض عملية الإنشاء هذه إلى "مصنع" (Factory).

* **التطبيق في JavaScript:**
    نقوم بإنشاء كلاس "مصنع" يحتوي على دالة وظيفتها إنشاء وإرجاع الكائنات المناسبة بناءً على المدخلات.

    **مثال: مصنع لإنشاء مستخدمين بأنواع مختلفة**
    ```javascript
    class BasicUser {
      constructor(name) { this.name = name; this.type = 'Basic'; }
    }
    class PremiumUser {
      constructor(name) { this.name = name; this.type = 'Premium'; }
    }

    class UserFactory {
      create(name, type = 'basic') {
        if (type === 'premium') {
          return new PremiumUser(name);
        } else {
          return new BasicUser(name);
        }
      }
    }
    
    // كيفية الاستخدام
    const factory = new UserFactory();
    const user1 = factory.create('Ahmed', 'basic');
    const user2 = factory.create('Sara', 'premium');

    console.log(user1); // BasicUser { name: 'Ahmed', type: 'Basic' }
    console.log(user2); // PremiumUser { name: 'Sara', type: 'Premium' }
    ```
**الفائدة:** هذا يفصل منطق الإنشاء عن الكود الرئيسي. إذا أردنا إضافة نوع مستخدم جديد (مثل `AdminUser`)، فإننا نعدل المصنع فقط، وليس كل جزء من الكود يقوم بإنشاء مستخدمين.

---

