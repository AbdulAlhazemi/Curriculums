## ⚙️ الوحدة 2: التطبيق العملي باستخدام GitHub Actions

### 📘 الدرس 2: إنشاء خط أنابيب CI أساسي لمشروع Node.js

#### 🧠 **ماذا ستتعلم**
* كيفية إنشاء ملف سير عمل لمشروع Node.js.
* كيفية استخدام الإجراءات الجاهزة `actions/checkout` و `actions/setup-node`.
* كيفية تشغيل `npm install` و `npm test` داخل سير العمل.
* كيفية اختبار الكود على إصدارات متعددة من Node.js باستخدام مصفوفة.

---
### 🎯 1. الهدف: أتمتة الاختبارات
لنفترض أن لدينا مشروع Node.js يحتوي على اختبارات آلية (مثل الذي أنشأناه في دورة الاختبار) و `package.json` يحتوي على سكربت `test`.

**الهدف:** إنشاء سير عمل (Workflow) في GitHub Actions يقوم تلقائيًا بتشغيل هذه الاختبارات في كل مرة يقوم فيها مطور بدفع كود جديد إلى المستودع. إذا فشلت الاختبارات، يجب أن يفشل سير العمل ويتم إبلاغ المطور.

---
### 📝 2. بناء ملف سير العمل خطوة بخطوة
سنقوم بإنشاء ملف جديد في مشروعنا بالمسار التالي: `.github/workflows/ci.yml`.

#### **الخطوة 1: الاسم والمُحفِّز (Name & Trigger)**
```yaml
name: Node.js CI

# شغل هذا السير عند كل push أو pull request يستهدف الفرع main
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
```
هذا يضمن أننا نختبر الكود قبل دمجه في الفرع الرئيسي وبعده.

#### **الخطوة 2: تعريف المهمة (Job)**
```yaml
jobs:
  # اسم المهمة، يمكن أن يكون أي شيء
  build:
    # سيتم تشغيل هذه المهمة على آلة افتراضية بنظام Ubuntu
    runs-on: ubuntu-latest
    
    # ... الخطوات ستأتي هنا
```

#### **الخطوة 3: تعريف الخطوات (Steps)**
هذه هي الإجراءات الفعلية التي ستقوم بها المهمة.
```yaml
    steps:
      # الخطوة الأولى: سحب نسخة من الكود
      - name: Checkout repository code
        uses: actions/checkout@v4

      # الخطوة الثانية: إعداد بيئة Node.js
      - name: Setup Node.js environment
        uses: actions/setup-node@v4
        with:
          node-version: '20.x' # يمكن تحديد أي إصدار

      # الخطوة الثالثة: تثبيت التبعيات
      - name: Install dependencies
        run: npm ci

      # الخطوة الرابعة: تشغيل الاختبارات
      - name: Run tests
        run: npm test
```
> **ملاحظة هامة:** نستخدم `npm ci` بدلاً من `npm install` في بيئات CI. الأمر `ci` أسرع ويقوم بتثبيت التبعيات بالضبط كما هي محددة في ملف `package-lock.json`، مما يضمن أن بيئة CI مطابقة تمامًا لبيئة المطور.

---
### 🧪 3. نصيحة متقدمة: مصفوفة الاختبار (Matrix)
ماذا لو أردت التأكد من أن تطبيقك يعمل على عدة إصدارات من Node.js (مثل 18 و 20)؟ يمكنك استخدام مصفوفة لتشغيل نفس المهمة عدة مرات بإعدادات مختلفة.

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    
    strategy:
      # سيقوم GitHub Actions بإنشاء مهمة منفصلة لكل إصدار في هذه المصفوفة
      matrix:
        node-version: [18.x, 20.x]

    steps:
      - uses: actions/checkout@v4
      - name: Use Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v4
        with:
          # استخدم المتغير من المصفوفة
          node-version: ${{ matrix.node-version }}
      - run: npm ci
      - run: npm test
```
الآن، عند تشغيل سير العمل، سترى مهمتين تعملان بالتوازي، واحدة لـ Node 18 والأخرى لـ Node 20.

---
