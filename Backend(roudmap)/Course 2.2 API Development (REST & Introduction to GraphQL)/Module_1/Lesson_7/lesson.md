## 🌐 الوحدة 1: مبادئ وتصميم واجهات RESTful API

### 📘 الدرس 7: توثيق واجهات API (API Documentation)

#### 🧠 **ماذا ستتعلم**
* لماذا يعتبر توثيق الـ API أمرًا حاسمًا.
* ما هي مواصفة OpenAPI (المعروفة سابقًا باسم Swagger).
* كيفية كتابة مستند OpenAPI أساسي لوصف واجهة API.
* كيفية استخدام `swagger-ui-express` لخدمة توثيق تفاعلي من تطبيق Express.

---
### 🤔 1. لماذا التوثيق مهم جدًا؟
توثيق الـ API هو **واجهة المستخدم للمطورين الآخرين**. إذا كان التوثيق سيئًا أو غير موجود، فلن يتمكن المطورون (سواء في فريقك أو عملاء خارجيين) من استخدام الـ API الخاص بك بفعالية.

* **الفوائد الرئيسية للتوثيق الجيد:**
    * **مصدر الحقيقة الوحيد (Single Source of Truth):** يعمل كعقد واضح بين فريق الواجهة الأمامية (frontend) والواجهة الخلفية (backend).
    * **تسهيل الانضمام (Faster Onboarding):** يساعد المطورين الجدد على فهم وبدء استخدام الـ API بسرعة.
    * **سهولة الاختبار والتصحيح:** يوفر مرجعًا واضحًا لكيفية عمل الـ API وما هي الاستجابات المتوقعة.
    * **تمكين الأتمتة:** يمكن استخدام مستندات التوثيق لإنشاء مكتبات عميل (Client SDKs) واختبارات تلقائيًا.

> **ببساطة:** واجهة API بدون توثيق تشبه جهازًا إلكترونيًا معقدًا بدون دليل استخدام. قد تكون قوية، ولكن لا أحد يعرف كيفية استخدامها.

---
### 📜 2. ما هي مواصفة OpenAPI (Swagger)؟
**مواصفة OpenAPI** هي معيار موحد ومفتوح المصدر لوصف وتوثيق واجهات RESTful API. هي تسمح لكل من البشر والآلات بفهم إمكانيات الخدمة دون الحاجة إلى الوصول إلى الكود المصدري.

* **Swagger:** كان هذا هو الاسم الأصلي للمواصفة. الآن، يشير اسم Swagger إلى مجموعة من الأدوات التي تطبق مواصفة OpenAPI (مثل Swagger UI, Swagger Editor).
* **التنسيق:** يتم كتابة مستند المواصفة إما بصيغة **JSON** أو **YAML**. غالبًا ما يُفضل YAML لسهولة قراءته للبشر.

---
### 📝 3. مثال على مستند OpenAPI بسيط
هذا مثال على كيفية توثيق أحد مسارات API الكتب الذي بنيناه، باستخدام صيغة YAML في ملف اسمه `swagger.yaml`.
```yaml
openapi: 3.0.0
info:
  title: My Book API
  description: A simple API to manage a collection of books.
  version: 1.0.0

servers:
  - url: http://localhost:3000/api

paths:
  /books:
    get:
      summary: Get a list of all books
      description: Returns an array of book objects.
      responses:
        '200':
          description: A successful response with a list of books.
          content:
            application/json:
              schema:
                type: array
                items:
                  type: object
                  properties:
                    id:
                      type: integer
                    title:
                      type: string
                    author:
                      type: string
```
---
### ⚙️ 4. إنشاء توثيق تفاعلي باستخدام Express
يمكننا استخدام حزمة `swagger-ui-express` لإنشاء صفحة ويب تفاعلية جميلة من ملف التوثيق الخاص بنا وخدمتها مباشرة من تطبيق Express.

#### **الخطوات:**
1.  **تثبيت الحزم:**
    ```bash
    npm install swagger-ui-express yamljs
    ```
    (`yamljs` هي حزمة مساعدة لتحليل ملفات YAML).

2.  **إنشاء ملف التوثيق:** أنشئ ملف `swagger.yaml` في جذر مشروعك والصق فيه الكود من المثال أعلاه.

3.  **إعداد Express في `index.js`:**
    ```javascript
    const express = require('express');
    const swaggerUi = require('swagger-ui-express');
    const YAML = require('yamljs');
    const swaggerDocument = YAML.load('./swagger.yaml');

    const app = express();
    // ... باقي إعداداتك ومساراتك ...

    // تركيب مسار التوثيق
    app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerDocument));

    // ... app.listen ...
    ```
4.  **التشغيل والاختبار:** شغل الخادم الخاص بك (`node index.js`) ثم اذهب في متصفحك إلى `http://localhost:3000/api-docs`. سترى الآن واجهة Swagger UI التفاعلية، والتي تعرض جميع نقاط النهاية الخاصة بك وتسمح لك حتى باختبارها مباشرة من المتصفح!

---