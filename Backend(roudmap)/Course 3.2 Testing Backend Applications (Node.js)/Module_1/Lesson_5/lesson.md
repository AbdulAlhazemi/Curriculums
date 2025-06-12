## 🧪 الوحدة 1: أساسيات الاختبار وإعداد البيئة

### 📘 الدرس 5: المحاكاة والتجسس (Mocking and Spying)

#### 🧠 **ماذا ستتعلم**
* لماذا نحتاج إلى "محاكاة" الاعتماديات في اختبارات الوحدة.
* الفرق المبدئي بين Mocks, Stubs, و Spies.
* كيفية إنشاء دالة محاكاة (mock function) بسيطة باستخدام `jest.fn()`.
* كيفية محاكاة وحدة (module) كاملة باستخدام `jest.mock()`.
* كيفية التحقق مما إذا تم استدعاء دالة محاكاة وبالوسائط الصحيحة.

---
### 🤔 1. مشكلة الاعتماديات (Dependencies)
في الدرس الثاني، قلنا أن اختبارات الوحدة يجب أن تكون **معزولة**. لكن في الواقع، معظم الدوال لا تعمل بمفردها، بل تعتمد على دوال أو وحدات أخرى.

* **مثال:** لديك دالة `registerUser(userData)` تقوم بحفظ المستخدم في قاعدة البيانات ثم ترسل له بريدًا إلكترونيًا ترحيبيًا.
    ```javascript
    function registerUser(user) {
      database.save(user);    // اعتمادية على قاعدة البيانات
      emailService.send(user.email, 'Welcome!'); // اعتمادية على خدمة البريد
      return true;
    }
    ```
* **المشكلة:** عند كتابة اختبار وحدة لدالة `registerUser`، نحن **لا نريد** الاتصال بقاعدة بيانات حقيقية أو إرسال بريد إلكتروني حقيقي. هذا سيجعل الاختبار بطيئًا، غير مستقر، ويعتمد على أنظمة خارجية.

---
### 👥 2. الحل: بدائل الاختبار (Test Doubles)
لحل هذه المشكلة، نستخدم ما يسمى "بدائل الاختبار"، وهي كائنات وهمية تحل محل الاعتماديات الحقيقية أثناء الاختبار. أشهر أنواعها:
* **Stub (بديل):** كائن بسيط يُرجع بيانات معدة مسبقًا.
* **Spy (جاسوس):** يلتف حول دالة حقيقية ويسجل معلومات حول كيفية استدعائها (كم مرة، بأي وسائط) دون تغيير سلوكها.
* **Mock (كائن محاكاة):** كائن "ذكي" يمكنك برمجته ليتصرف بطرق معينة (مثل الـ Stub) ويسجل كيفية استخدائه (مثل الـ Spy).

> **في Jest:** يوفر Jest أداة قوية تسمى **"دوال المحاكاة" (Mock Functions)** يمكنها أداء جميع هذه الأدوار، مما يبسط العملية. الفكرة الرئيسية هي **استبدال الشيء الحقيقي بشيء وهمي يمكننا التحكم فيه ومراقبته**.

---
### ✨ 3. المحاكاة باستخدام Jest
#### **أ. محاكاة وحدة كاملة (`jest.mock()`)**
هذه هي الطريقة الأكثر شيوعًا وفعالية. يمكنك أن تطلب من Jest استبدال وحدة كاملة بنسخة محاكاة.

**لنفترض أن لدينا هذه الملفات:**
**`emailService.js` (الاعتمادية التي نريد محاكاتها)**
```javascript
// هذا يرسل بريدًا حقيقيًا
const sendEmail = (to, subject, body) => {
  console.log(`Sending real email to ${to}...`);
  // ... منطق إرسال البريد الفعلي ...
};
module.exports = { sendEmail };
```

**`signup.js` (الوحدة التي نختبرها)**
```javascript
const { sendEmail } = require('./emailService');

const signup = (email, password) => {
  // ... منطق إنشاء المستخدم ...
  console.log(`User ${email} signed up.`);
  sendEmail(email, 'Welcome to our app!');
  return true;
};
module.exports = { signup };
```
**ملف الاختبار `signup.test.js`**
```javascript
const { signup } = require('./signup');
const { sendEmail } = require('./emailService');

// 1. اطلب من Jest استبدال الوحدة الحقيقية بنسخة محاكاة
jest.mock('./emailService');

describe('signup function', () => {
  it('should call the email service after a successful signup', () => {
    // Arrange
    const testEmail = 'test@example.com';
    const testPassword = 'password123';
    
    // Act
    signup(testEmail, testPassword);

    // Assert
    // الآن، sendEmail ليست الدالة الحقيقية، بل هي دالة محاكاة من Jest
    
    // هل تم استدعاء الدالة؟
    expect(sendEmail).toHaveBeenCalled();
    
    // كم مرة تم استدعاؤها؟
    expect(sendEmail).toHaveBeenCalledTimes(1);
    
    // ما هي الوسائط التي تم استدعاؤها بها؟
    expect(sendEmail).toHaveBeenCalledWith('test@example.com', 'Welcome to our app!');
  });
});
```
بهذه الطريقة، اختبرنا منطق دالة `signup` وتأكدنا من أنها تستدعي خدمة البريد بشكل صحيح، كل ذلك **دون إرسال بريد إلكتروني حقيقي واحد**.

---
