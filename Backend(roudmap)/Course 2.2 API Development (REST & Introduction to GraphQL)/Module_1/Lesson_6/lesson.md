## 🌐 الوحدة 1: مبادئ وتصميم واجهات RESTful API

### 📘 الدرس 6: بناء واجهة RESTful API باستخدام Express.js

#### 🧠 **ماذا ستتعلم**
* كيفية تطبيق مبادئ REST عمليًا في تطبيق Express.
* كيفية هيكلة مشروع API باستخدام المسارات (Routes) والمتحكمات (Controllers).
* بناء جميع عمليات CRUD (إنشاء، قراءة، تحديث، حذف) لمورد معين.
* إرسال استجابات JSON برموز حالة HTTP مناسبة.

---
### 🎯 1. الهدف: بناء API لإدارة "الكتب"
في هذا الدرس، سنقوم ببناء واجهة API بسيطة لإدارة مجموعة من الكتب. ستمكننا هذه الـ API من عرض قائمة بالكتب، عرض كتاب معين، إضافة كتاب جديد، تحديثه، وحذفه.

للحفاظ على التركيز على Express و REST، سنستخدم **مصفوفة في الذاكرة** كم قاعدة بيانات مؤقتة.

**لنبدأ بهذه البيانات الأولية:**
```javascript
// يمكنك وضع هذا في ملف الـ controller الخاص بك
let books = [
  { id: 1, title: 'The Hobbit', author: 'J.R.R. Tolkien' },
  { id: 2, title: '1984', author: 'George Orwell' }
];
let nextId = 3;
```
---
### 📂 2. هيكل المشروع
سنتبع الهيكل المنظم الذي تعلمناه في دورة Express:
```
/my-book-api
|-- /controllers
|   |-- bookController.js
|-- /routes
|   |-- bookRoutes.js
|-- index.js
|-- package.json
```
---
### ⚙️ 3. تطبيق نقاط النهاية (Endpoints)

#### **أ. الإعداد الرئيسي (`index.js`)**
هذا الملف سيقوم بتجميع أجزاء التطبيق معًا.
```javascript
const express = require('express');
const app = express();
const bookRoutes = require('./routes/bookRoutes');

// Middleware لقراءة أجسام طلبات JSON
app.use(express.json());

// تركيب مسارات الكتب على المسار الرئيسي /api/books
app.use('/api/books', bookRoutes);

const PORT = 3000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```

#### **ب. منطق التحكم (`controllers/bookController.js`)**
هنا نكتب منطق كل عملية.
```javascript
// بياناتنا المؤقتة
let books = [
  { id: 1, title: 'The Hobbit', author: 'J.R.R. Tolkien' },
  { id: 2, title: '1984', author: 'George Orwell' }
];
let nextId = 3;

// GET /api/books
exports.getAllBooks = (req, res) => {
  res.status(200).json(books);
};

// GET /api/books/:id
exports.getBookById = (req, res) => {
  const book = books.find(b => b.id === parseInt(req.params.id));
  if (!book) return res.status(404).send('The book with the given ID was not found.');
  res.status(200).json(book);
};

// POST /api/books
exports.createBook = (req, res) => {
  const newBook = {
    id: nextId++,
    title: req.body.title,
    author: req.body.author
  };
  books.push(newBook);
  res.status(201).json(newBook);
};

// PUT /api/books/:id
exports.updateBook = (req, res) => {
  const book = books.find(b => b.id === parseInt(req.params.id));
  if (!book) return res.status(404).send('The book was not found.');
  
  book.title = req.body.title;
  book.author = req.body.author;
  res.status(200).json(book);
};

// DELETE /api/books/:id
exports.deleteBook = (req, res) => {
  const bookIndex = books.findIndex(b => b.id === parseInt(req.params.id));
  if (bookIndex === -1) return res.status(404).send('The book was not found.');

  const deletedBook = books.splice(bookIndex, 1);
  res.status(200).json(deletedBook);
};
```

#### **ج. تعريف المسارات (`routes/bookRoutes.js`)**
هذا الملف يربط كل مسار بالدالة المناسبة في الـ controller.
```javascript
const express = require('express');
const router = express.Router();
const bookController = require('../controllers/bookController');

// GET /api/books
router.get('/', bookController.getAllBooks);

// GET /api/books/:id
router.get('/:id', bookController.getBookById);

// POST /api/books
router.post('/', bookController.createBook);

// PUT /api/books/:id
router.put('/:id', bookController.updateBook);

// DELETE /api/books/:id
router.delete('/:id', bookController.deleteBook);

module.exports = router;
```
---