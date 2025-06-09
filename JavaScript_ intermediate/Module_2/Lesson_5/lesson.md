# الوحدة 2: الأحداث والتفاعلية

## الدرس 5: التحقق من صحة النماذج باستخدام جافاسكريبت


🧠 **ماذا ستتعلم**
*	كيفية التحقق من صحة إدخال المستخدم باستخدام جافاسكريبت
*	كيفية عرض رسائل الخطأ ومنع إرسال النموذج
*	الفرق بين التحقق المدمج والتحقق المخصص

---

📋 **1. لماذا التحقق من صحة النماذج؟**

يضمن التحقق من صحة النماذج أن المستخدمين يقدمون مدخلات متوقعة وقابلة للاستخدام. بدونه، قد تحصل على:
*	حقول فارغة
*	عناوين بريد إلكتروني غير صالحة
*	كلمات مرور غير متطابقة

يساعد التحقق من الصحة على حماية تطبيقك وتحسين تجربة المستخدم.

---

🔍 **2. التحقق المدمج في HTML**

يمكنك البدء بسمات HTML مثل:
```html
<input type="email" required />
```
هذه تمنع الإرسال ما لم يتم ملء الحقل بعنوان بريد إلكتروني صالح. لكنها محدودة وليست قابلة للتخصيص بشكل كبير.

---

💻 **3. التحقق المخصص باستخدام جافاسكريبت**

يمكنك التحكم باستخدام جافاسكريبت عن طريق الاستماع إلى حدث `submit` الخاص بالنموذج والتحقق من القيم يدويًا.

مثال:
```html
<form id="signupForm">
  <input id="email" type="email" placeholder="Email" />
  <input id="password" type="password" placeholder="Password" />
  <button type="submit">Sign Up</button>
</form>
<p id="errorMessage"></p>
```
```javascript
const form = document.querySelector("#signupForm");
const email = document.querySelector("#email");
const password = document.querySelector("#password");
const error = document.querySelector("#errorMessage");

form.addEventListener("submit", (event) => {
  event.preventDefault(); // منع النموذج من الإرسال (إعادة تحميل الصفحة)

  if (!email.value.includes("@")) {
    error.textContent = "Please enter a valid email.";
  } else if (password.value.length < 6) {
    error.textContent = "Password must be at least 6 characters.";
  } else {
    error.textContent = "";
    console.log("Form submitted successfully!");
    // يمكنك الآن إرسال البيانات إلى الخادم هنا
  }
});
```

---

✨ **4. التحقق في الوقت الفعلي (اختياري)**

يمكنك التحقق من الإدخال أثناء كتابة المستخدم باستخدام حدث `input`:
```javascript
email.addEventListener("input", () => {
  if (!email.value.includes("@")) {
    email.style.borderColor = "red";
  } else {
    email.style.borderColor = "green";
  }
});
```

---

🛑 **5. عرض رسائل الخطأ**

لتجربة أفضل:
*	أظهر رسائل خطأ محددة ومفيدة.
*	تجنب عرض أخطاء متعددة في نفس الوقت.
*	امسح الخطأ عند تصحيح الإدخال.

---

🧠 **النقاط الرئيسية**
*	استخدم `event.preventDefault()` للتعامل مع النماذج يدويًا.
*	تحقق من صحة الحقول باستخدام جافاسكريبت قبل الإرسال.
*	قدم دائمًا للمستخدمين ملاحظات مفيدة حول الخطأ.

---