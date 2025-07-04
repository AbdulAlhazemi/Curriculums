## 📬 الوحدة 1: أساسيات طوابير الرسائل

### 📘 الدرس 8: التعامل مع الأخطاء وإعادة المحاولة

#### 🧠 **ماذا ستتعلم**
* أنواع الأخطاء التي يمكن أن تحدث في المستهلك.
* أهمية آلية الإقرار (Acknowledgement).
* مفهوم طابور الرسائل الميتة (Dead-Letter Queue - DLQ).
* استراتيجيات إعادة محاولة المهام الفاشلة.

---
### 🤔 1. لماذا يختلف التعامل مع الأخطاء هنا؟
في طلب HTTP المتزامن، إذا حدث خطأ، يحصل المستخدم على استجابة خطأ فورية. لكن في النظام غير المتزامن، يكون المستخدم قد تلقى بالفعل استجابة ناجحة ("تم استلام طلبك"). الخطأ يحدث لاحقًا، في الخلفية، داخل أحد العمال (Workers).

**التحدي:** كيف نضمن عدم فقدان المهمة الفاشلة، وكيف نمنعها من تعطيل بقية الطابور؟

---
### 🤝 2. آلية الإقرار (Acknowledgement)
هذه هي الآلية الأساسية لضمان الموثوقية في RabbitMQ.
عندما يسحب المستهلك رسالة من الطابور، لا يتم حذفها فورًا. بدلاً من ذلك، يتم "حجزها" وتصبح غير مرئية للمستهلكين الآخرين.

* **`ack` (Acknowledge):** بعد أن **ينجح** المستهلك في معالجة الرسالة بالكامل، يرسل إشارة `ack` إلى RabbitMQ. عندها فقط، يقوم RabbitMQ بحذف الرسالة بشكل دائم.
* **`nack` (Negative Acknowledge):** إذا **فشل** المستهلك في معالجة الرسالة، يجب عليه إرسال إشارة `nack`. هذا يخبر RabbitMQ: "لقد فشلت في هذه المهمة، يرجى التصرف". يمكن لـ RabbitMQ بعد ذلك إما إعادة الرسالة إلى الطابور لمحاولة أخرى، أو التخلص منها.

> **ببساطة:** تخيلها مثل **البريد المسجل**. يجب عليك **التوقيع (ack)** لتأكيد استلامك للطرد بنجاح. إذا رفضت التوقيع أو لم تكن في المنزل (nack)، يعود ساعي البريد بالطرد إلى مكتب البريد (الوسيط) ليحاول توصيله مرة أخرى لاحقًا.

---
### 🔄 3. استراتيجية إعادة المحاولة (Retries)
قد تفشل مهمة بسبب مشكلة مؤقتة (مثل تعطل واجهة API خارجية للحظات). نريد إعادة المحاولة. لكن إعادة وضعها في الطابور فورًا قد يسبب حلقة لا نهائية إذا استمرت المشكلة.

* **الحل الأفضل: التراجع الأسي (Exponential Backoff):**
    هي استراتيجية إعادة محاولة ذكية. بدلاً من إعادة المحاولة كل ثانية، يتم زيادة فترة الانتظار بين كل محاولة فاشلة.
    * المحاولة 1: بعد 10 ثوانٍ.
    * المحاولة 2: بعد 30 ثانية.
    * المحاولة 3: بعد دقيقتين.
    وهكذا. هذا يعطي النظام الخارجي الذي به مشكلة وقتًا للتعافي. توفر مكتبات مثل BullMQ هذه الميزة بشكل مدمج.

---
### 🪦 4. طابور الرسائل الميتة (Dead-Letter Queue - DLQ)
**ماذا لو فشلت الرسالة بعد كل محاولات إعادة المحاولة؟**
لا نريدها أن تبقى عالقة في الطابور الرئيسي إلى الأبد وتمنع معالجة الرسائل الأخرى. هذه الرسالة تسمى أحيانًا "الرسالة السامة" (Poison Pill).

**الحل هو DLQ:**
* **التعريف:** هو طابور خاص يتم توجيه الرسائل التي فشلت بشكل نهائي إليه.
* **الغرض:** يعمل كـ "مقبرة" للمهام الفاشلة. هو يمنع الرسائل السامة من تعطيل النظام.
* **دورة العمل:** يمكن للمطورين أو أنظمة المراقبة فحص الرسائل في الـ DLQ لتشخيص سبب المشكلة، إصلاح الخطأ، وربما إعادة معالجة الرسائل يدويًا.

---
