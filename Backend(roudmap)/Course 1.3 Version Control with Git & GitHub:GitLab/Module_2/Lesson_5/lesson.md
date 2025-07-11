# الوحدة 2: الأساسيات العملية في Git
## الدرس 5: مراجعة تاريخ التعديلات باستخدام `git log`

🧠 **ماذا ستتعلم**
* كيفية عرض تاريخ `Commits` باستخدام الأمر `git log`.
* فهم معلومات كل `Commit` مثل معرفه، المؤلف، التاريخ، والرسالة.
* التنقل بين السجلات وإيقاف العرض عند الحاجة.

---

### 🧾 1. ما هو `git log`؟
الأمر `git log` يعرض قائمة بــ `Commits` التي تم حفظها في المشروع، مرتبة من الأحدث إلى الأقدم.

كل سجل (`Commit`) يحتوي على:
* معرف فريد (hash).
* اسم المؤلف وتاريخ الإنشاء.
* رسالة `Commit` التي تشرح التعديل.

---

### 🧾 2. استخدام `git log`
لتشغيل الأمر، نفذ:
```bash
git log
```
سترى قائمة طويلة من `Commits`. لإيقاف العرض مؤقتًا، اضغط مفتاح `q` للخروج من شاشة السجل.

---

### 🧾 3. خيارات مفيدة مع `git log`
* **عرض السجل بشكل مختصر (سطر واحد لكل `Commit`):**
  ```bash
  git log --oneline
  ```
* **عرض السجل مع التعديلات التي تمت في كل `Commit`:**
  ```bash
  git log -p
  ```

---