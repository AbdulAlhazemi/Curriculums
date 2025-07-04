## 🌐 الوحدة 1: مبادئ وتصميم واجهات RESTful API

### 📘 الدرس 4: صيغ البيانات في واجهات برمجة التطبيقات (API Data Formats)

#### 🧠 **ماذا ستتعلم**
* لماذا نحتاج إلى صيغة بيانات موحدة للتواصل بين الأنظمة.
* مقدمة في صيغة XML.
* نظرة تفصيلية على صيغة JSON، الصيغة الأكثر شيوعًا اليوم.
* مقارنة بين JSON و XML ولماذا يُفضل استخدام JSON في معظم واجهات الويب الحديثة.

---
### 🤔 1. لماذا نحتاج إلى صيغة بيانات موحدة؟
عندما يتواصل تطبيقان (مثل تطبيق جوال وخادم)، فإنهما يحتاجان إلى التحدث بـ "لغة" مشتركة لفهم البيانات المتبادلة. صيغة البيانات هي هذه اللغة. إذا أرسل الخادم بيانات بصيغة معينة، يجب أن يكون العميل قادرًا على فهمها وتفسيرها بشكل صحيح، والعكس صحيح.

---
### 📜 2. الصيغة القديمة: XML
**XML (eXtensible Markup Language)** هي لغة توصيف كانت شائعة جدًا في الماضي لواجهات برمجة التطبيقات (خاصة مع SOAP). تستخدم وسوم (tags) لتعريف البيانات، بشكل مشابه لـ HTML.

**مثال على بيانات مستخدم بصيغة XML:**
```xml
<user>
  <id>123</id>
  <name>Jameel</name>
  <email>jameel@example.com</email>
</user>
```
**خصائصها:** قوية، صارمة، لكنها مطولة (verbose) ومعقدة نسبيًا في التحليل.

---
### ✨ 3. الصيغة الحديثة: JSON
**JSON (JavaScript Object Notation)** هي صيغة خفيفة الوزن لتبادل البيانات. أصبحت المعيار الفعلي لمعظم واجهات RESTful API الحديثة.

**نفس بيانات المستخدم بصيغة JSON:**
```json
{
  "id": 123,
  "name": "Jameel",
  "email": "jameel@example.com"
}
```
**خصائصها:** موجزة، سهلة القراءة للبشر، وسهلة التحليل للآلات، خاصة وأنها صيغة جافاسكريبت أصلية.

---
### ⚖️ 4. مقارنة: JSON مقابل XML

| الخاصية | JSON | XML |
| :--- | :--- | :--- |
| **الإطناب (Verbosity)** | موجز وأقل كلامًا. | مطوّل ويحتوي على وسوم فتح وإغلاق. |
| **سهولة القراءة** | أسهل وأوضح للبشر. | قد يكون معقدًا ومتشعبًا. |
| **التحليل (Parsing)** | أسرع وأسهل، خاصة في بيئة جافاسكريبت. | يتطلب محلل (parser) مخصص وأبطأ نسبيًا. |
| **أنواع البيانات** | يدعم الأرقام، النصوص، القيم المنطقية، المصفوفات، والكائنات. | يتعامل مع كل شيء كنص ويتطلب مخطط (schema) لتعريف الأنواع. |
| **الاستخدام** | مسيطر في واجهات RESTful API وتطبيقات الويب الحديثة. | لا يزال يستخدم في أنظمة الشركات الكبرى، ملفات الإعدادات، و SOAP. |

**الخلاصة:** بالنسبة لمعظم تطبيقات الويب اليوم، JSON هو الخيار الأفضل بفضل بساطته وسرعته وتوافقه الأصلي مع جافاسكريبت.

---
### ⚙️ 5. كيف يعمل هذا مع Express؟
لقد تعاملنا بالفعل مع JSON في دورة Express!
* **عند إرسال استجابة:** دالة `res.json(someObject)` تقوم تلقائيًا بتحويل كائن جافاسكريبت إلى نص JSON وتعيين ترويسة `Content-Type` إلى `application/json`.
* **عند استقبال طلب:** الـ Middleware `express.json()` يقوم تلقائيًا بتحليل جسم الطلب الوارد إذا كانت ترويسة `Content-Type` هي `application/json`، ويجعله متاحًا ككائن جافاسكريبت في `req.body`.

---