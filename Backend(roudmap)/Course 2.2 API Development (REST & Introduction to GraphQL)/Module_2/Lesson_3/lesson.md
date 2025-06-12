## 🚀 الوحدة 2: مقدمة في GraphQL

### 📘 الدرس 3: إعداد خادم GraphQL أساسي مع Node.js

#### 🧠 **ماذا ستتعلم**
* كيفية إعداد مشروع Node.js لخادم GraphQL.
* الحزم الأساسية المطلوبة (`express`, `graphql`, `express-graphql`).
* كيفية تعريف مخطط (Schema) بسيط باستخدام `buildSchema`.
* كيفية كتابة كائن المُحلِّلات (Resolvers) الجذري.
* كيفية ربط المخطط والمحللات مع Express لإنشاء نقطة نهاية GraphQL.
* كيفية استخدام واجهة GraphiQL التفاعلية لاختبار الـ API.

---
### 🧱 1. الحزم التي سنحتاجها
لبناء خادمنا، سنحتاج إلى ثلاث حزم رئيسية من npm:
1.  **`express`**: إطار العمل الذي نعرفه لتشغيل خادم الويب.
2.  **`graphql`**: المكتبة الأساسية التي تحتوي على منطق GraphQL الأساسي وتسمح بتنفيذ الاستعلامات.
3.  **`express-graphql`**: هي الـ Middleware التي تعمل كجسر بين Express ومكتبة `graphql`. هي من تنشئ نقطة نهاية HTTP التي تفهم وتستجيب لطلبات GraphQL.

---
### ⚙️ 2. خطوات بناء الخادم

#### **الخطوة 1: إعداد المشروع**
افتح الطرفية ونفذ الأوامر التالية:
```bash
# إنشاء مجلد جديد والدخول إليه
mkdir my-graphql-server
cd my-graphql-server

# تهيئة مشروع npm
npm init -y

# تثبيت الحزم المطلوبة
npm install express graphql express-graphql
```

#### **الخطوة 2: إنشاء ملف الخادم**
أنشئ ملفًا جديدًا باسم `server.js`.

#### **الخطوة 3: كتابة الكود (`server.js`)**
افتح ملف `server.js` وأضف الكود التالي، الذي سنشرحه خطوة بخطوة:

```javascript
const express = require('express');
const { graphqlHTTP } = require('express-graphql');
const { buildSchema } = require('graphql');

// الخطوة 1: تعريف المخطط (Schema) باستخدام لغة تعريف المخطط
// نستخدم الـ backticks (``) لكتابة نص متعدد الأسطر
const schema = buildSchema(`
  type Query {
    hello: String
  }
`);

// الخطوة 2: تعريف المُحلِّل (Resolver)
// يجب أن يكون كائنًا يتطابق هيكله مع المخطط
const root = {
  // اسم الدالة هنا "hello" يطابق اسم الحقل في "Query"
  hello: () => {
    // هذه الدالة تُرجع البيانات لهذا الحقل
    return 'Hello, world! This is my first GraphQL API.';
  }
};

// الخطوة 3: إنشاء خادم Express ونقطة نهاية GraphQL
const app = express();
app.use('/graphql', graphqlHTTP({
  schema: schema,
  rootValue: root,
  graphiql: true, // تفعيل واجهة GraphiQL التفاعلية
}));

const PORT = 4000;
app.listen(PORT, () => {
  console.log(`Running a GraphQL API server at http://localhost:${PORT}/graphql`);
});
```

---
### 🧪 3. اختبار الـ API باستخدام GraphiQL
`GraphiQL` هي واجهة تطوير مدمجة (IDE) تعمل في المتصفح، تأتي مع `express-graphql` وتسمح لك باختبار الـ API الخاص بك بسهولة.

1.  **شغل الخادم** من طرفيتك:
    ```bash
    node server.js
    ```
2.  **افتح متصفحك** واذهب إلى العنوان: `http://localhost:4000/graphql`.
3.  سترى واجهة GraphiQL. في اللوحة اليسرى، اكتب الاستعلام التالي:
    ```graphql
    query {
      hello
    }
    ```
4.  اضغط على زر التشغيل (▶).
5.  في اللوحة اليمنى، يجب أن ترى الاستجابة التالية بصيغة JSON:
    ```json
    {
      "data": {
        "hello": "Hello, world! This is my first GraphQL API."
      }
    }
    ```

---
