## 🗃️ الوحدة 2: استعلامات SQL المتقدمة وتصميم قواعد البيانات

### 📘 الدرس 1: استعلامات SQL المتقدمة (JOINs & Aggregations)

#### 🧠 **ماذا ستتعلم**
* الغرض من جملة `JOIN` لربط الجداول.
* كيفية استخدام `INNER JOIN` و `LEFT JOIN`.
* ما هي الدوال التجميعية (`COUNT`, `SUM`, `AVG`).
* كيفية تجميع النتائج باستخدام `GROUP BY`.
* كيفية فلترة المجموعات باستخدام `HAVING`.

---
### 📋 1. تحضير البيانات للمثال
لفهم `JOINs`، نحتاج إلى جدولين مترابطين. لنقم بإنشاء جدول للمؤلفين (`authors`) وجدول للكتب (`books`).

**قم بتنفيذ الأوامر التالية في `psql` داخل قاعدة بياناتك:**

**1. إنشاء الجداول:**
```sql
CREATE TABLE authors (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL
);

CREATE TABLE books (
    id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    author_id INTEGER REFERENCES authors(id) -- This is the Foreign Key
);
```
**2. إدراج البيانات:**
```sql
INSERT INTO authors (name) VALUES ('George Orwell'), ('J.R.R. Tolkien'), ('F. Scott Fitzgerald');

INSERT INTO books (title, author_id) VALUES
('1984', 1),
('Animal Farm', 1),
('The Hobbit', 2),
('The Lord of the Rings', 2);
```
> **ملاحظة:** لدينا 3 مؤلفين، لكن المؤلف 'F. Scott Fitzgerald' ليس لديه أي كتب في جدولنا. هذا سيساعدنا على فهم الفرق بين أنواع `JOIN`.

---
### 🔗 2. ربط الجداول - الأمر `JOIN`
نحتاج في كثير من الأحيان إلى بيانات من جداول متعددة في استعلام واحد (مثلاً، اسم الكتاب واسم المؤلف معًا). جملة `JOIN` هي التي تسمح لنا بذلك.

#### **`INNER JOIN` (الربط الداخلي)**
يُرجع هذا الربط فقط السجلات التي لها قيم متطابقة في **كلا الجدولين**.

**مثال:** جلب جميع الكتب مع أسماء مؤلفيها.
```sql
SELECT
    books.title,
    authors.name
FROM books
INNER JOIN authors ON books.author_id = authors.id;
```
**النتيجة:**
| title | name |
| :--- | :--- |
| 1984 | George Orwell |
| Animal Farm | George Orwell |
| The Hobbit | J.R.R. Tolkien |
| The Lord of the Rings| J.R.R. Tolkien |

> لاحظ أن 'F. Scott Fitzgerald' لم يظهر لأنه ليس لديه كتب مطابقة في جدول `books`.

#### **`LEFT JOIN` (الربط الأيسر)**
يُرجع هذا الربط **جميع السجلات من الجدول الأيسر** (الذي يأتي بعد `FROM`)، والسجلات المتطابقة من الجدول الأيمن. إذا لم يكن هناك تطابق، تكون قيمة حقول الجدول الأيمن `NULL`.

**مثال:** جلب جميع المؤلفين والكتب التي كتبوها (إن وجدت).
```sql
SELECT
    authors.name,
    books.title
FROM authors
LEFT JOIN books ON authors.id = books.author_id;
```
**النتيجة:**
| name | title |
| :--- | :--- |
| George Orwell | 1984 |
| George Orwell | Animal Farm |
| J.R.R. Tolkien | The Hobbit |
| J.R.R. Tolkien | The Lord of the Rings|
| F. Scott Fitzgerald| *NULL* |

> لاحظ أن 'F. Scott Fitzgerald' ظهر الآن، ولكن قيمة `title` الخاصة به هي `NULL` لأنه ليس لديه كتب.

---
### 📊 3. الدوال التجميعية (Aggregate Functions)
هي دوال تقوم بإجراء عملية حسابية على مجموعة من الصفوف وتُرجع قيمة واحدة ملخصة.

| الدالة | الوصف | مثال |
| :--- | :--- | :--- |
| `COUNT(column)` | تحسب عدد الصفوف. | `SELECT COUNT(*) FROM books;` (ستُرجع 4) |
| `SUM(column)` | تحسب مجموع قيم عمود رقمي. | `SELECT SUM(price) FROM products;` |
| `AVG(column)` | تحسب متوسط قيم عمود رقمي. | `SELECT AVG(price) FROM products;` |
| `MAX(column)` | تجد القيمة القصوى في عمود. | `SELECT MAX(price) FROM products;` |
| `MIN(column)` | تجد القيمة الدنيا في عمود. | `SELECT MIN(price) FROM products;` |

---
### 🧺 4. تجميع النتائج - `GROUP BY` و `HAVING`
#### **`GROUP BY`**
تُستخدم مع الدوال التجميعية لتقسيم الصفوف إلى مجموعات أصغر.

**مثال:** حساب عدد الكتب لكل مؤلف.
```sql
SELECT
    authors.name,
    COUNT(books.id) AS number_of_books -- AS لتعيين اسم مستعار للعمود
FROM authors
LEFT JOIN books ON authors.id = books.author_id
GROUP BY authors.name;
```
**النتيجة:**
| name | number_of_books |
| :--- | :--- |
| F. Scott Fitzgerald| 0 |
| George Orwell | 2 |
| J.R.R. Tolkien | 2 |

#### **`HAVING`**
تستخدم **لفلترة المجموعات** بعد أن يتم إنشاؤها بواسطة `GROUP BY`. لا يمكن استخدام `WHERE` لفلترة نتائج الدوال التجميعية.

**مثال:** عرض المؤلفين الذين لديهم **أكثر من كتاب واحد فقط**.
```sql
SELECT
    authors.name,
    COUNT(books.id) AS number_of_books
FROM authors
JOIN books ON authors.id = books.author_id
GROUP BY authors.name
HAVING COUNT(books.id) > 1;
```
**النتيجة:**
| name | number_of_books |
| :--- | :--- |
| George Orwell | 2 |
| J.R.R. Tolkien | 2 |

---
