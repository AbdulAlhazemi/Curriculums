# الوحدة 3: العمل مع الفروع (Branches)
## الدرس 4: الاستراتيجيات الشائعة لإدارة الفروع (Git Flow و Feature Branching)

🧠 **ماذا ستتعلم**
* أهمية تنظيم الفروع في المشاريع.
* الفرق بين Git Flow و Feature Branching.
* متى تستخدم كل استراتيجية.

---

### 🧾 1. لماذا نحتاج إلى استراتيجيات لتنظيم الفروع؟
في المشاريع الصغيرة، قد لا تشعر بالفوضى عند استخدام الفروع.
لكن في المشاريع المتوسطة أو الكبيرة، تتداخل الميزات، والإصلاحات، والإصدارات.

❗ لذلك نحتاج إلى استراتيجية تُنظم العمل الجماعي وتُحدد الغرض من كل فرع.

---

### 🧾 2. ما هي استراتيجية Feature Branching؟
🎯 **Feature Branching** تعني:
لكل ميزة أو تعديل، نُنشئ فرعًا جديدًا مستقلًا.

**الخطوات:**
1.  إنشاء فرع: `feature/search-bar`
2.  تطوير الميزة
3.  اختبارها
4.  دمجها في `main` عند الانتهاء

✅ بسيطة وسهلة.
✅ مناسبة للفرق الصغيرة أو المتوسطة.

---

### 🧾 3. ما هي استراتيجية Git Flow؟
🎯 **Git Flow** هي استراتيجية أكثر تنظيمًا للمشاريع الكبيرة.
تُقسّم العمل إلى فروع رئيسية وفروع فرعية، ولكل منها غرض محدد.

| نوع الفرع | الغرض |
| :--- | :--- |
| `main` | يحتوي على النسخ المستقرة فقط |
| `develop` | يحتوي على التعديلات الجارية |
| `feature/*` | لتطوير ميزات جديدة |
| `release/*` | لإعداد إصدارات جاهزة للنشر |
| `hotfix/*` | لإصلاحات عاجلة على الإنتاج |

---

### 🧾 4. متى تستخدم كل استراتيجية؟

| الحالة | الاستراتيجية المناسبة |
| :--- | :--- |
| مشروع بسيط بفريق صغير | Feature Branching |
| مشروع كبير بفريق متوزع | Git Flow |
| مشاريع تجريبية أو شخصية | أي منهما أو لا شيء |

---