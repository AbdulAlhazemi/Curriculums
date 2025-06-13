## 🏆 المشروع النهائي: بناء خط أنابيب CI/CD متكامل

### 🎯 الهدف
إنشاء خط أنابيب كامل للتكامل والنشر المستمر (CI/CD) لمشروع Express API باستخدام **GitHub Actions**. سيقوم سير العمل (Workflow) تلقائيًا ببناء التطبيق، وتشغيل مجموعة الاختبارات الكاملة (بما في ذلك الاختبارات التكاملية التي تتطلب قاعدة بيانات)، وفي النهاية، محاكاة عملية النشر إلى خادم.

---

### 🏗️ أساس المشروع
يجب عليك استخدام **مشروع Express CRUD API** الذي قمت ببنائه واختباره في الدورات السابقة. من الضروري أن يكون هذا المشروع:
1.  موجودًا في مستودع (repository) على **GitHub**.
2.  يحتوي على مجموعة اختبارات (`npm test`) تتضمن اختبارات تكاملية تتصل بقاعدة بيانات PostgreSQL.

---

### 📝 مهام المشروع

#### **الجزء الأول: إعداد المستودع (Repository Setup)**
قبل كتابة سير العمل، يجب عليك إعداد مستودعك على GitHub:
1.  اذهب إلى `Settings` > `Secrets and variables` > `Actions`.
2.  أنشئ **سرًا جديدًا (New repository secret)**:
    * **Name:** `POSTGRES_PASSWORD`
    * **Value:** كلمة المرور التي تستخدمها لمستخدم `postgres` في قاعدة بياناتك.
3.  أنشئ **متغيرًا جديدًا (New repository variable)**:
    * **Name:** `POSTGRES_DB`
    * **Value:** اسم قاعدة بيانات الاختبار الخاصة بك (e.g., `books_api_test`).

---
#### **الجزء الثاني: بناء خط أنابيب التكامل المستمر (CI)**
أنشئ ملفًا جديدًا في مشروعك بالمسار `.github/workflows/main.yml`.

**1. تعريف سير العمل والمُحفِّز:**
عرّف سير عمل يتم تشغيله عند كل `push` أو `pull_request` يستهدف الفرع `main`.

**2. إعداد مهمة الاختبار (`test`):**
هذه هي المهمة الرئيسية التي ستتأكد من جودة الكود.
* **تشغيل قاعدة بيانات:** استخدم ميزة `services` في GitHub Actions لتشغيل حاوية Docker جاهزة لـ PostgreSQL. هذا ينشئ قاعدة بيانات مؤقتة تعمل فقط أثناء تنفيذ المهمة.
* **خطوات المهمة:**
    أ.  **`actions/checkout@v4`**: سحب نسخة من الكود.
    ب. **`actions/setup-node@v4`**: إعداد بيئة Node.js.
    ج. **`npm ci`**: تثبيت التبعيات بشكل نظيف.
    د.  **`npm test`**: تشغيل مجموعة الاختبارات. يجب عليك تمرير الأسرار والمتغيرات كمتغيرات بيئة إلى هذه الخطوة حتى يتمكن تطبيقك من الاتصال بقاعدة بيانات الخدمة.

**مثال على ملف `main.yml` للجزء الثاني:**
```yaml
name: Node.js CI/CD

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    
    # تشغيل خدمة PostgreSQL في الخلفية لهذه المهمة
    services:
      postgres:
        image: postgres:14-alpine
        env:
          POSTGRES_USER: postgres
          POSTGRES_PASSWORD: ${{ secrets.POSTGRES_PASSWORD }}
          POSTGRES_DB: ${{ vars.POSTGRES_DB }}
        ports:
          - 5432:5432
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5

    steps:
      - uses: actions/checkout@v4
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20.x'
          
      - name: Install Dependencies
        run: npm ci

      - name: Run Tests
        # تمرير الأسرار والمتغيرات إلى سكربت الاختبار
        run: npm test
        env:
          NODE_ENV: test
          PGHOST: localhost
          PGUSER: postgres
          PGDATABASE: ${{ vars.POSTGRES_DB }}
          PGPASSWORD: ${{ secrets.POSTGRES_PASSWORD }}
          PGPORT: 5432
```

---
#### **الجزء الثالث: إضافة مهمة النشر (Conceptual Deployment)**
أضف مهمة ثانية إلى نفس الملف لمحاكاة عملية النشر.

1.  **اسم المهمة:** `deploy`.
2.  **التبعية:** اجعلها تعتمد على نجاح مهمة `test` باستخدام `needs: test`.
3.  **الشرط:** اجعلها تعمل فقط عند الدفع إلى الفرع `main` باستخدام `if: github.ref == 'refs/heads/main'`.
4.  **الخطوات:** أضف خطوات بسيطة تستخدم `run` لطباعة رسائل تحاكي عملية النشر، مثل:
    ```yaml
    steps:
      - name: Deploying to production
        run: |
          echo "🚀 Deployment started..."
          echo "✅ Application deployed successfully!"
    ```

---
### ✅ معايير التقييم
* سير عمل GitHub Actions يعمل بنجاح عند كل `push` إلى `main`.
* مهمة `test` تقوم بإعداد Node.js وخدمة PostgreSQL بنجاح.
* نجاح مجموعة الاختبارات (`npm test`) داخل بيئة CI، مما يثبت اتصالها بقاعدة البيانات.
* ظهور علامة صح خضراء (✔) على الـ commit الخاص بك في GitHub.
* مهمة `deploy` تعمل فقط بعد نجاح مهمة `test` وعلى الفرع `main` فقط.

---
### 🚀 الخطوة الأولى
1.  ابدأ بإنشاء ملف سير العمل `main.yml` في مشروعك.
2.  ركز على إعداد مهمة `test` أولاً مع خدمة PostgreSQL.
3.  قم بدفع الملف إلى GitHub وشاهد سير العمل وهو يعمل (أو يفشل) في علامة التبويب "Actions". قم بتصحيح الأخطاء حتى تنجح مهمة الاختبار.
4.  بعد ذلك، أضف مهمة `deploy` المفاهيمية.

**تهانينا!** بإكمال هذا المشروع، تكون قد طبقت دورة DevOps كاملة، من كتابة الكود والمبادئ التصميمية، إلى الاختبار الآلي، وصولًا إلى بناء خط أنابيب جاهز للنشر المستمر.