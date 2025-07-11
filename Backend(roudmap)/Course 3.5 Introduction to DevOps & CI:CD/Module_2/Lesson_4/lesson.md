## ⚙️ الوحدة 2: التطبيق العملي باستخدام GitHub Actions

### 📘 الدرس 4: متغيرات البيئة والأسرار في CI/CD

#### 🧠 **ماذا ستتعلم**
* مشكلة كتابة الإعدادات الحساسة مباشرة في الكود.
* الفرق بين متغيرات البيئة (Variables) والأسرار (Secrets).
* كيفية إنشاء واستخدام متغيرات البيئة في GitHub Actions.
* كيفية إنشاء واستخدام الأسرار في GitHub Actions.

---
### 🤔 1. المشكلة: الإعدادات والأسرار في الكود
تحتاج تطبيقاتنا وخطوط الأنابيب الخاصة بنا إلى معلومات لكي تعمل، مثل:
* سلسلة الاتصال بقاعدة البيانات.
* مفاتيح API لخدمات خارجية (مثل خدمة إرسال بريد إلكتروني).
* مفتاح SSH خاص لنشر الكود على خادمنا.

كتابة هذه القيم مباشرة في الكود أو في ملف سير العمل (`.yml`) هي **ممارسة سيئة للغاية**. إنها تشكل خطرًا أمنيًا كبيرًا (أي شخص لديه حق الوصول إلى الكود يمكنه سرقة هذه الأسرار) وتجعل من الصعب تغيير الإعدادات بين بيئات العمل المختلفة (التطوير، الإنتاج).

---
### 💡 2. الحل: متغيرات البيئة والأسرار
يوفر GitHub Actions طريقتين لإدارة هذه القيم بشكل آمن ومنظم.

* **Variables (متغيرات البيئة):**
    * **تُستخدم لـ:** المعلومات **غير الحساسة** التي قد تتغير بين عمليات التشغيل.
    * **أمثلة:** اسم المستخدم للخادم (`SERVER_USER`)، عنوان IP للخادم (`SERVER_IP`)، أو اسم بيئة التشغيل (`NODE_ENV=production`).
    * **طبيعتها:** يتم تخزينها كنص عادي ويمكن طباعتها في سجلات سير العمل.

* **Secrets (الأسرار):**
    * **تُستخدم لـ:** المعلومات **الحساسة** التي يجب أن تظل مشفرة.
    * **أمثلة:** كلمة مرور قاعدة البيانات (`DB_PASSWORD`)، توكن API، مفتاح SSH الخاص (`SSH_PRIVATE_KEY`).
    * **طبيعتها:** يتم تشفيرها بواسطة GitHub **ولا يمكن عرضها أبدًا** في سجلات سير العمل أو بعد حفظها. إذا قمت بطباعة سر في السجل، سيقوم GitHub تلقائيًا باستبداله بعلامات `***`.

---
### 📝 3. كيفية الاستخدام في GitHub Actions

#### **الإنشاء في واجهة GitHub:**
1.  اذهب إلى مستودعك على GitHub.
2.  انقر على **Settings**.
3.  في القائمة الجانبية، اذهب إلى **Secrets and variables** ثم اختر **Actions**.
4.  سترى قسمين: واحد لـ **Secrets** والآخر لـ **Variables**.
5.  انقر على "New repository secret" أو "New repository variable" لإضافة قيمة جديدة.

#### **الاستخدام في ملف سير العمل:**
* للوصول إلى **سر**، استخدم صيغة: `${{ secrets.YOUR_SECRET_NAME }}`
* للوصول إلى **متغير**، استخدم صيغة: `${{ vars.YOUR_VARIABLE_NAME }}`

**مثال على مهمة نشر تستخدم كليهما:**
```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    needs: test
    steps:
      - name: Deploy to production server
        uses: appleboy/ssh-action@master
        with:
          # استخدام متغيرات غير حساسة
          host: ${{ vars.SERVER_IP }}
          username: ${{ vars.SERVER_USER }}
          
          # استخدام سر مشفر للمعلومات الحساسة
          key: ${{ secrets.SSH_PRIVATE_KEY }} 
          
          script: |
            echo "Starting deployment..."
            # ... أوامر النشر ...
```
---

