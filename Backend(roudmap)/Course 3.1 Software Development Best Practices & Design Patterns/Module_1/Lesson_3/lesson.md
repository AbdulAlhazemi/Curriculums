## 📐 الوحدة 1: مبادئ الكود النظيف وأنماط التصميم

### 📘 الدرس 3: مبادئ SOLID

#### 🧠 **ماذا ستتعلم**
* ما هي مبادئ SOLID الخمسة وما هو الغرض منها.
* معنى كل مبدأ من المبادئ الخمسة.
* أمثلة عملية بلغة جافاسكريبت توضح كيفية تطبيق هذه المبادئ.

---
### 🤔 1. ما هي مبادئ SOLID؟
SOLID هو اختصار يمثل خمسة من أهم المبادئ الأساسية في البرمجة الكائنية (Object-Oriented Design)، وضعها روبرت مارتن ("Uncle Bob"). الهدف من هذه المبادئ هو مساعدتك على كتابة كود **مرن (Flexible)**، **قابل للصيانة (Maintainable)**، و**قابل للتطوير (Scalable)**.

---
### ☝️ 2. مبدأ المسؤولية الواحدة (Single Responsibility Principle - SRP)
**"يجب أن يكون للكلاس سبب واحد فقط للتغيير."**

هذا يعني أن كل كلاس أو وحدة يجب أن تكون مسؤولة عن وظيفة واحدة فقط.

* **مثال سيئ:**
    ```javascript
    class User {
      constructor(name, email) {
        this.name = name;
        this.email = email;
      }
      // هذه الدالة تخلط بين بيانات المستخدم ومنطق قاعدة البيانات
      saveToDatabase() {
        // ... code to connect and save to DB
      }
    }
    ```
    هذا الكلاس لديه سببان للتغيير: تغيير بيانات المستخدم، أو تغيير طريقة الحفظ في قاعدة البيانات.

* **مثال جيد:**
    ```javascript
    class User {
      constructor(name, email) {
        this.name = name;
        this.email = email;
      }
    }
    // كلاس منفصل ومسؤوليته فقط التعامل مع قاعدة البيانات
    class UserRepository {
      save(user) {
        // ... code to save user to DB
      }
    }
    ```
---
### ↔️ 3. مبدأ الفتح/الإغلاق (Open/Closed Principle - OCP)
**"يجب أن تكون الكيانات البرمجية (كلاسات، دوال، إلخ) مفتوحة للتوسيع، ولكن مغلقة للتعديل."**

هذا يعني أنه يجب أن تكون قادرًا على إضافة وظائف جديدة دون تغيير الكود الموجود.

* **مثال سيئ:**
    ```javascript
    function printReport(reportData, type) {
      if (type === 'PDF') {
        // ... logic to print PDF
      } else if (type === 'CSV') {
        // ... logic to print CSV
      }
      // لإضافة نوع جديد (مثل XML)، يجب تعديل هذه الدالة
    }
    ```
* **مثال جيد:**
    ```javascript
    // نستخدم استراتيجيات مختلفة لكل نوع
    class PdfPrinter { print(data) { /* ... */ } }
    class CsvPrinter { print(data) { /* ... */ } }

    function printReport(reportData, printer) {
      // لا نحتاج لتعديل هذه الدالة لإضافة نوع جديد
      printer.print(reportData);
    }
    ```
---
### 🔄 4. مبدأ استبدال ليسكوف (Liskov Substitution Principle - LSP)
**"يجب أن تكون الأنواع الفرعية قابلة للاستبدال بأنواعها الأساسية دون التأثير على صحة البرنامج."**

إذا كان لديك كلاس `Bird`، وكلاس `Penguin` يرث منه، فيجب أن تتمكن من استخدام كائن `Penguin` في أي مكان يتوقع فيه كائن `Bird` دون أن يحدث خطأ.

* **مثال سيئ:**
    ```javascript
    class Bird { fly() { /* ... */ } }
    class Penguin extends Bird {
      fly() {
        throw new Error("Penguins can't fly!"); // هذا يكسر التوقعات
      }
    }
    ```
* **مثال جيد:** إعادة الهيكلة بحيث لا تُرغم الأنواع الفرعية على تنفيذ وظائف لا تدعمها.
    ```javascript
    class Bird { /* ... */ }
    class FlyingBird extends Bird { fly() { /* ... */ } }
    class SwimmingBird extends Bird { swim() { /* ... */ } }
    class Penguin extends SwimmingBird { /* ... */ }
    ```
---
### 🔪 5. مبدأ فصل الواجهة (Interface Segregation Principle - ISP)
**"لا يجب إجبار العميل على الاعتماد على واجهات (interfaces) لا يستخدمها."**

من الأفضل أن يكون لديك عدة واجهات صغيرة ومتخصصة بدلاً من واجهة واحدة كبيرة وعامة.

* **مثال سيئ:** واجهة `Worker` كبيرة تحتوي على `work()` و `eat()`. كلاس `Robot` قد يحتاج لتنفيذ `work()` لكن `eat()` لا معنى لها.
* **مثال جيد:** فصلها إلى واجهتين: `IWorkable` و `IEatable`. يمكن للكلاسات تنفيذ الواجهات التي تحتاجها فقط.

---
### 🔃 6. مبدأ عكس التبعية (Dependency Inversion Principle - DIP)
**"الوحدات عالية المستوى لا يجب أن تعتمد على الوحدات منخفضة المستوى. كلاهما يجب أن يعتمد على تجريدات (abstractions)."**

هذا المبدأ يشجع على استخدام "حقن التبعية" (Dependency Injection).

* **مثال سيئ (اقتران وثيق - Tight Coupling):**
    ```javascript
    class EmailNotifier {
      send(message) { /* ... */ }
    }
    class Order {
      constructor() {
        // Order تعتمد مباشرة على EmailNotifier
        this.notifier = new EmailNotifier();
      }
      process() {
        this.notifier.send("Order processed");
      }
    }
    ```
* **مثال جيد (اقتران مرن - Loose Coupling):**
    ```javascript
    // نمرر الـ Notifier كـ "تبعية" من الخارج
    class Order {
      constructor(notifier) {
        this.notifier = notifier;
      }
      process() {
        this.notifier.send("Order processed");
      }
    }
    // الآن يمكننا بسهولة استخدام أي نوع من Notifier
    const emailNotifier = new EmailNotifier();
    const smsNotifier = new SmsNotifier();
    const order1 = new Order(emailNotifier);
    const order2 = new Order(smsNotifier);
    ```
---
