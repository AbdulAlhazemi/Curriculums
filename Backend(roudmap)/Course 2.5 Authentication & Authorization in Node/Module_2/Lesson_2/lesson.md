## 🔑 الوحدة 2: المصادقة القائمة على التوكن (Token-Based Authentication)

### 📘 الدرس 2: تشريح توكن JWT

#### 🧠 **ماذا ستتعلم**
* الأجزاء الثلاثة المكونة لتوكن JWT: الترويسة، الحمولة، والتوقيع.
* الصيغة العامة لتوكن JWT (`xxxxx.yyyyy.zzzzz`).
* الغرض من الترويسة (Header).
* الغرض من الحمولة (Payload) وأنواع الادعاءات (Claims).
* الدور الحاسم للتوقيع (Signature) في التحقق من صحة التوكن.

---
### 🏗️ 1. هيكل توكن JWT
توكن JWT هو في الحقيقة مجرد سلسلة نصية طويلة. إذا نظرت عن كثب، ستجد أنه يتكون دائمًا من ثلاثة أجزاء مفصولة بنقاط (`.`):

`HEADER`.`PAYLOAD`.`SIGNATURE`

**مثال على توكن:**
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

> **نقطة أمان هامة:** الجزآن الأولان (الترويسة والحمولة) هما مجرد كائنات JSON تم ترميزها باستخدام **Base64Url**. هذا **ترميز (encoding) وليس تشفيرًا (encryption)**. هذا يعني أن أي شخص يمكنه فك ترميز هذين الجزأين ورؤية ما بداخلهما. لذلك، **لا تضع أبدًا معلومات حساسة (مثل كلمات المرور) داخل توكن JWT.**

---
### 🧩 2. الأجزاء الثلاثة بالتفصيل

#### **الجزء الأول: الترويسة (Header)**
هذا الجزء يحتوي على بيانات وصفية حول التوكن نفسه. عادة ما يحتوي على معلومتين:
* `alg`: خوارزمية التوقيع المستخدمة (مثل `HS256`).
* `typ`: نوع التوكن، وهو دائمًا `JWT`.

**مثال على كائن JSON للترويسة:**
```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```
يتم بعد ذلك ترميز هذا الكائن باستخدام Base64Url ليشكل الجزء الأول من التوكن.

#### **الجزء الثاني: الحمولة (Payload)**
هذا الجزء يحتوي على **الادعاءات (Claims)**. الادعاءات هي معلومات حول الكيان (عادة المستخدم) وبيانات وصفية إضافية.

* **أنواع الادعاءات:**
    * **مسجلة (Registered):** ادعاءات قياسية مثل `sub` (Subject - معرف المستخدم)، `exp` (Expiration Time - وقت انتهاء صلاحية التوكن)، و `iat` (Issued At - وقت إصدار التوكن).
    * **عامة (Public):** ادعاءات يمكن تعريفها بحرية.
    * **خاصة (Private):** ادعاءات مخصصة يتم الاتفاق عليها بين العميل والخادم (مثل `role: 'admin'`).

**مثال على كائن JSON للحمولة:**
```json
{
  "sub": "user123",
  "name": "Jameel",
  "role": "admin",
  "exp": 1678886400
}
```
يتم ترميز هذا الكائن أيضًا باستخدام Base64Url ليشكل الجزء الثاني من التوكن.

#### **الجزء الثالث: التوقيع (Signature)**
هذا هو **الجزء الأمني** في التوكن. يتم إنشاؤه على الخادم ويستخدم للتحقق من أن التوكن لم يتم العبث به أو تغييره أثناء النقل.

**كيف يتم إنشاؤه؟**
يتم إنشاء التوقيع عن طريق أخذ:
1.  الترويسة المرمزة.
2.  نقطة (`.`).
3.  الحمولة المرمزة.
4.  تجزئة كل ما سبق باستخدام الخوارزمية المحددة في الترويسة مع **مفتاح سري (Secret Key)** لا يعرفه أحد سوى الخادم.

`التوقيع = HASH_ALGORITHM(encodedHeader + '.' + encodedPayload, secretKey)`

**كيفية التحقق:** عندما يستقبل الخادم التوكن، فإنه يعيد إنشاء التوقيع بنفسه باستخدام نفس الطريقة. إذا تطابق التوقيع الذي أنشأه مع التوقيع الموجود في التوكن، فهذا يعني أن التوكن أصلي ولم يتم تعديله.

---
