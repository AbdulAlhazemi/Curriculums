# الوحدة 1: مقدمة إلى التحكم في الإصدارات
## الدرس 2: أنواع أنظمة التحكم في الإصدارات

🧠 **ماذا ستتعلم**
* الفرق بين الأنظمة المحلية والمركزية والموزعة.
* مميزات وعيوب كل نوع.
* لماذا Git يُصنف كنظام موزّع.

---

### 🧾 1. ما هي أنواع أنظمة التحكم؟

#### ✅ أولًا: النظام المحلي (Local VCS)
* التعديلات تُسجل **محليًا فقط** على جهاز واحد.
* أمثلة قديمة: RCS (Revision Control System).
* **العيب**: لا يدعم العمل الجماعي بسهولة.

---

#### ✅ ثانيًا: النظام المركزي (Centralized VCS)
* يوجد **خادم مركزي** يحتوي على جميع ملفات المشروع.
* المطورون يتصلون بالخادم للحصول على آخر إصدار.
* أمثلة: CVS، Subversion (SVN).
* 🟥 **العيب:** إذا توقف الخادم، يتوقف العمل للجميع!

---

#### ✅ ثالثًا: النظام الموزع (Distributed VCS)
* كل مطور يمتلك **نسخة كاملة** من المشروع (ملفات + تاريخ كامل).
* العمل لا يعتمد دائمًا على الاتصال بخادم مركزي.
* **أشهر مثال:** Git.
* 🟢 **الميزة:** حتى بدون إنترنت، يمكن حفظ التعديلات والعودة إليها لاحقًا.

---

### 📊 مقارنة سريعة:
| النوع | يحتاج اتصال دائم؟ | نسخ احتياطية متعددة؟ | يدعم العمل الجماعي؟ |
| :--- | :--- | :--- | :--- |
| المحلي | لا | لا | لا |
| المركزي | نعم | لا | نعم |
| الموزع (مثل Git) | لا | نعم | نعم |

---