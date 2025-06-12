## 🏆 المشروع النهائي: ربط واجهة API بقاعدة بيانات PostgreSQL

### 🎯 الهدف
إعادة هيكلة مشروع واجهة برمجة التطبيقات (API) الخاص بالكتب (من دورة Express) لاستبدال تخزين البيانات في الذاكرة (المصفوفة) بقاعدة بيانات PostgreSQL حقيقية. سيثبت هذا المشروع قدرتك على تصميم مخطط قاعدة بيانات، كتابة استعلامات SQL، وربط تطبيق Node.js بقاعدة بيانات علائقية.

---

### 📝 أجزاء المشروع
المشروع مقسم إلى جزأين: التنفيذ باستخدام SQL الخام أولاً، ثم إعادة الهيكلة اختياريًا باستخدام ORM.

---
### **الجزء الأول: التكامل باستخدام SQL الخام ومكتبة `pg`**
في هذا الجزء، سنتفاعل مع قاعدة البيانات مباشرة باستخدام استعلامات SQL.

#### **1. تصميم المخطط (Schema)**
سنحتاج إلى جدولين: واحد للمؤلفين والآخر للكتب، مع علاقة "واحد لكثير" بينهما (مؤلف واحد له العديد من الكتب).
* **جدول `authors`:**
    * `id` (SERIAL, PRIMARY KEY)
    * `name` (VARCHAR, NOT NULL)
* **جدول `books`:**
    * `id` (SERIAL, PRIMARY KEY)
    * `title` (VARCHAR, NOT NULL)
    * `author_id` (INTEGER, FOREIGN KEY references `authors.id`)

#### **2. إنشاء الجداول (DDL)**
اتصل بقاعدة بياناتك باستخدام `psql` ونفذ أوامر `CREATE TABLE` التالية:
```sql
CREATE TABLE authors (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL
);

CREATE TABLE books (
    id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    author_id INTEGER,
    CONSTRAINT fk_author
        FOREIGN KEY(author_id) 
        REFERENCES authors(id)
        ON DELETE SET NULL -- Or ON DELETE CASCADE
);
```

#### **3. تعديل المتحكمات (Controllers)**
هذا هو الجزء البرمجي الأساسي. ستحتاج إلى تعديل دوال الـ controller الخاصة بك لاستبدال منطق التعامل مع المصفوفة بمنطق `pool.query()` للتفاعل مع PostgreSQL.

* **`getAllBooks`:** ستحتاج إلى استخدام `INNER JOIN` لجلب عنوان الكتاب واسم المؤلف معًا.
* **`getBookById`:** ستحتاج أيضًا إلى `JOIN` واستخدام استعلام مُمَعلم (parameterized query) مع `WHERE id = $1`.
* **`createBook`:** ستأخذ `title` و `author_id` من `req.body` وتستخدم `INSERT INTO`.
* **`updateBook`:** ستستخدم `UPDATE ... WHERE id = $1`.
* **`deleteBook`:** ستستخدم `DELETE FROM ... WHERE id = $1`.

---
### **الجزء الثاني (اختياري): إعادة الهيكلة باستخدام ORM - Sequelize**
هذا الجزء يوضح كيف يمكن لـ ORM تبسيط الكود.

**1. إعداد Sequelize:**
* قم بتثبيت `sequelize`, `pg`, `pg-hstore`.
* أنشئ ملف اتصال `sequelize.js`.
* عرّف موديل `Author` وموديل `Book`.
* عرّف العلاقة بينهما: `Author.hasMany(Book)` و `Book.belongsTo(Author)`.

**2. إعادة كتابة المتحكمات:**
* استبدل كل استدعاء `pool.query(...)` بدوال Sequelize المقابلة.
* **مثال (لجلب جميع الكتب مع مؤلفيها):**
    ```javascript
    // بدلاً من كتابة JOIN يدويًا
    const books = await Book.findAll({
      include: Author // Sequelize سيقوم بالـ JOIN تلقائيًا
    });
    res.json(books);
    ```

---
### ✅ معايير التقييم
* مخطط قاعدة بيانات صحيح ومنظم.
* واجهة API تعمل بشكل كامل حيث تقوم عمليات CRUD بالتفاعل مع قاعدة البيانات بنجاح.
* الاستخدام الصحيح للاستعلامات المُمَعلمَة في الجزء الأول لمنع حقن SQL.
* (اختياري) إعادة هيكلة ناجحة باستخدام Sequelize، مما يدل على فهم مفاهيم الـ ORM.

---
### 🚀 الخطوة الأولى
1.  ابدأ بإنشاء قاعدة بيانات جديدة لمشروعك (e.g., `CREATE DATABASE book_api;`).
2.  باستخدام `psql`، اتصل بقاعدة البيانات الجديدة ونفذ أوامر `CREATE TABLE` لإنشاء جدولي `authors` و `books`.
3.  ابدأ بتعديل أول نقطة نهاية في الـ controller، وهي `getAllBooks`، لجلب البيانات من قاعدة البيانات باستخدام `JOIN`.

أتمنى لك كل التوفيق في مشروعك النهائي!