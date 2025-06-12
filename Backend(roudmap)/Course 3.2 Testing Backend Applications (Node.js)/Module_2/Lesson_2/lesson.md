## 🧪 الوحدة 2: اختبارات التكامل و E2E

### 📘 الدرس 2: اختبار نقاط نهاية Express API مع Supertest

#### 🧠 **ماذا ستتعلم**
* ما هي مكتبة `supertest` ولماذا نستخدمها لاختبار واجهات API.
* كيفية إعداد `supertest` في بيئة اختبار Jest.
* كيفية كتابة اختبار لنقطة نهاية `GET`.
* كيفية كتابة اختبار لنقطة نهاية `POST`، بما في ذلك إرسال البيانات.
* كيفية إجراء تأكيدات (assertions) على حالة الاستجابة وجسمها.

---
### 🤔 1. التحدي والأداة: Supertest
**التحدي:** كيف يمكننا، من داخل ملف الاختبار، إرسال طلبات HTTP برمجية (مثل `GET`, `POST`) إلى تطبيق Express الخاص بنا، ثم التحقق من صحة استجابة HTTP التي يعيدها؟

**الحل هو `supertest`:**
هي مكتبة شهيرة توفر واجهة عالية المستوى لاختبار خوادم HTTP. هي تسمح لك بـ "قيادة" تطبيق Express الخاص بك برمجيًا. أفضل ميزة فيها هي أنها لا تتطلب تشغيل الخادم على منفذ حقيقي، بل يمكنها اختبار التطبيق مباشرة، مما يجعل الاختبارات أسرع وأسهل في الإعداد.

---
### ⚙️ 2. إعداد Supertest

**الخطوة 1: التثبيت**
يجب تثبيتها كـ "تبعية تطوير" (`dev dependency`).
```bash
npm install --save-dev supertest
```

**الخطوة 2: الإعداد في ملف الاختبار**
1.  قم باستيراد `request` من مكتبة `supertest`.
2.  قم باستيراد كائن `app` من تطبيق Express الخاص بك. (يجب أن يكون ملف `app.js` أو `server.js` يقوم بتصدير كائن `app`).

**مثال للهيكل:**
```javascript
// file: books.test.js
const request = require('supertest');
const app = require('../app'); // افترض أن ملفك الرئيسي هو app.js
```

---
### ✍️ 3. كتابة اختبارات الـ API

#### **أ. اختبار نقطة نهاية `GET`**
لنفترض أننا نختبر `GET /api/books` التي من المفترض أن تعيد مصفوفة من الكتب.
```javascript
describe('GET /api/books', () => {
  it('should respond with a list of books', async () => {
    // إرسال الطلب إلى التطبيق
    const response = await request(app).get('/api/books');

    // التأكيد على رمز الحالة (Status Code)
    expect(response.statusCode).toBe(200);

    // التأكيد على نوع جسم الاستجابة
    expect(response.body).toBeInstanceOf(Array);
  });
});
```

#### **ب. اختبار نقطة نهاية `POST`**
لنفترض أننا نختبر `POST /api/books` التي تنشئ كتابًا جديدًا. نستخدم دالة `.send()` لإرفاق جسم الطلب.
```javascript
describe('POST /api/books', () => {
  it('should create a new book and respond with it', async () => {
    const newBookData = { title: 'The Test Book', author: 'Jest' };
    
    const response = await request(app)
      .post('/api/books')
      .send(newBookData); // إرسال البيانات في جسم الطلب
      
    // التأكيد على رمز الحالة (201 Created)
    expect(response.statusCode).toBe(201);
    
    // التأكيد على أن جسم الاستجابة يحتوي على البيانات المرسلة
    // toMatchObject يتحقق من أن الكائن يحتوي (على الأقل) على هذه الخصائص
    expect(response.body).toMatchObject(newBookData);

    // التأكيد على وجود خاصية 'id' التي أضافتها قاعدة البيانات
    expect(response.body).toHaveProperty('id');
  });
});
```
---
### 🔗 4. التكامل مع قاعدة بيانات الاختبار
كما تعلمنا في الدرس السابق، يجب أن تكون قاعدة البيانات في حالة نظيفة ومعروفة قبل كل اختبار.

**مثال يدمج `supertest` مع خطافات Jest لإدارة قاعدة البيانات:**
```javascript
const request = require('supertest');
const app = require('../app');
const db = require('../db'); // كائن الاتصال بقاعدة البيانات

describe('Book Endpoints', () => {

  // قبل كل اختبار في هذه المجموعة، نظّف جدول الكتب
  beforeEach(async () => {
    await db.query('DELETE FROM books');
  });

  // بعد انتهاء جميع الاختبارات في هذا الملف، أغلق الاتصال بقاعدة البيانات
  afterAll(async () => {
    await db.end();
  });

  it('should create a book and then be able to retrieve it', async () => {
    // 1. Act (POST)
    await request(app)
      .post('/api/books')
      .send({ title: 'My New Book', author: 'Me' });

    // 2. Act (GET)
    const response = await request(app).get('/api/books');

    // 3. Assert
    expect(response.body).toHaveLength(1);
    expect(response.body[0].title).toBe('My New Book');
  });
});
```

---

