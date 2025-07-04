## 💻 الوحدة 1: أساسيات أنظمة التشغيل وواجهة سطر الأوامر

### 📘 الدرس 5: عرض محتويات الملفات (Viewing File Contents)

#### 🧠 **ماذا ستتعلم**
* كيفية عرض المحتوى الكامل لملف باستخدام `cat`.
* كيفية تصفح الملفات الكبيرة صفحة بصفحة باستخدام `less`.
* كيفية عرض الأسطر الأولى من ملف باستخدام `head`.
* كيفية عرض الأسطر الأخيرة من ملف ومراقبته في الوقت الفعلي باستخدام `tail`.

---
### 🛠️ قبل أن نبدأ
لجعل الأمثلة عملية، لنقم بإنشاء ملف نصي يحتوي على عدة أسطر. افتح الطرفية ونفذ الأمر التالي لإنشاء ملف اسمه `story.txt`:
```bash
echo -e "Once upon a time in a digital kingdom,\nthere lived a curious user.\nThey wanted to master the command line.\nEach day, they learned a new command.\nFirst, they learned to navigate.\nThen, they learned to manage files.\nNow, they are learning to view them.\nThis was a great step forward.\nThey felt more powerful with each lesson.\nThe end." > story.txt
```
الآن أصبح لديك ملف `story.txt` يحتوي على 10 أسطر يمكننا استخدامه في الأمثلة التالية.

---
### 🐱 1. عرض الملف بالكامل - الأمر `cat`
الأمر `cat` (اختصار لـ **cat**enate) يستخدم لطباعة محتوى ملف بالكامل إلى الطرفية. إنه مناسب جدًا للملفات الصغيرة.

**مثال:**
```bash
cat story.txt
```
**الناتج:** سيطبع جميع الأسطر العشرة من الملف `story.txt` على شاشتك مباشرة.

---
### 📄 2. تصفح الملفات الكبيرة - الأمر `less`
عندما يكون الملف كبيرًا جدًا، فإن استخدام `cat` سيؤدي إلى تدفق النص بسرعة على الشاشة. الأمر `less` هو الحل الأمثل، حيث يسمح لك بتصفح الملف صفحة بصفحة.

**مثال:**
```bash
less story.txt
```
عند تنفيذ هذا الأمر، ستفتح واجهة عرض خاصة. يمكنك استخدام المفاتيح التالية للتنقل:
* **مفاتيح الأسهم (↑/↓)** أو **j/k**: للتمرير سطرًا بسطر.
* **مفتاح المسافة (Spacebar)**: للانتقال إلى الصفحة التالية.
* **/كلمة**: للبحث عن كلمة معينة داخل الملف.
* **q**: للخروج من `less` والعودة إلى الطرفية.

> **لماذا `less`؟** لأنه "أكثر" من `more` (`less` is more than `more`). `less` هو نسخة محسّنة من أمر قديم يسمى `more`، حيث يسمح `less` بالتمرير للخلف والأمام، وهو ما لا يفعله `more` بسهولة.

---
### 🔝 3. عرض بداية الملف - الأمر `head`
يستخدم الأمر `head` لعرض الجزء العلوي (البداية) من الملف. بشكل افتراضي، يعرض أول 10 أسطر.

**مثال:**
```bash
# عرض أول 10 أسطر (بشكل افتراضي)
head story.txt

# لعرض أول 3 أسطر فقط، استخدم الخيار -n
head -n 3 story.txt
```

---
### 🔚 4. عرض نهاية الملف - الأمر `tail`
يستخدم الأمر `tail` لعرض الجزء السفلي (النهاية) من الملف. بشكل افتراضي، يعرض آخر 10 أسطر. هذا الأمر مفيد جدًا لمراقبة ملفات السجل (log files).

**مثال:**
```bash
# عرض آخر 10 أسطر (بشكل افتراضي)
tail story.txt

# لعرض آخر 4 أسطر فقط
tail -n 4 story.txt
```
> **ميزة قوية:** الخيار `-f` (follow) يسمح لك بمراقبة الملف في الوقت الفعلي. أي سطر جديد تتم إضافته إلى الملف سيظهر مباشرة في طرفيتك. هذا لا يقدر بثمن عند مراقبة سجلات الخادم.
> ```bash
> # افتح نافذة طرفية أخرى وأضف نصًا جديدًا للملف لترى التحديث
> tail -f story.txt
> ```
> للخروج من وضع المراقبة، اضغط `Ctrl + C`.

---
