## 🗃️ الوحدة 1: أساسيات قواعد البيانات العلائقية و SQL

### 📘 الدرس 2: مقدمة في لغة الاستعلام المهيكلة (SQL)

#### 🧠 **ماذا ستتعلم**
* ما هي لغة SQL وما هو دورها الأساسي.
* معنى كون SQL لغة "تعريفية" (Declarative).
* الفئات الرئيسية لأوامر SQL: DDL, DML, و DQL.
* أمثلة بسيطة لكل فئة من الأوامر.

---
### 🤔 1. ما هي لغة SQL؟
**SQL** (اختصار لـ **S**tructured **Q**uery **L**anguage) هي اللغة القياسية والموحدة المستخدمة للتواصل مع قواعد البيانات العلائقية وإدارتها. إذا أردت أن تطلب من قاعدة بيانات أن تخزن بيانات، أو تعدلها، أو تحذفها، أو تسترجعها، فإنك تستخدم لغة SQL. إنها "لغة التخاطب" مع قواعد البيانات.

> **نقطة مهمة:** SQL هي لغة **تعريفية (Declarative)**. هذا يعني أنك تخبر قاعدة البيانات **ماذا** تريد (`what`)، وليس **كيف** يجب أن تفعل ذلك (`how`). أنت تقول "أعطني جميع المستخدمين الذين تزيد أعمارهم عن 30 عامًا"، وقاعدة البيانات هي التي تقرر أفضل طريقة للبحث عنهم وإرجاعهم.

---
### 📚 2. اللغات الفرعية لـ SQL
يتم تجميع أوامر SQL عادةً في فئات فرعية بناءً على وظيفتها. أهمها:

| الاختصار | الاسم الكامل | الغرض | أشهر الأوامر |
| :--- | :--- | :--- | :--- |
| **DQL** | Data Query Language | **استرجاع واستعلام** البيانات. | `SELECT` |
| **DML** | Data Manipulation Language | **التلاعب بالبيانات** نفسها (إضافة، تحديث، حذف). | `INSERT`, `UPDATE`, `DELETE` |
| **DDL** | Data Definition Language | **تعريف هيكل** قاعدة البيانات (إنشاء جداول، تعديلها، حذفها). | `CREATE TABLE`, `ALTER TABLE`, `DROP TABLE` |
| **DCL** | Data Control Language | **التحكم في صلاحيات** وصول المستخدمين. | `GRANT`, `REVOKE` |

في البداية، سنركز على DDL, DML, و DQL.

---
### ✨ 3. لمحة عن أوامر SQL
لنعطيك فكرة عن شكل اللغة، إليك مثال بسيط لكل فئة رئيسية:

#### **DQL - استرجاع البيانات**
```sql
-- جلب عمودي الاسم والبريد الإلكتروني لجميع المستخدمين
SELECT name, email FROM users;
```

#### **DML - التلاعب بالبيانات**
```sql
-- إضافة صف جديد (مستخدم جديد) إلى جدول المستخدمين
INSERT INTO users (name, email) VALUES ('Fatima', 'fatima@example.com');
```

#### **DDL - تعريف البيانات**
```sql
-- إنشاء جدول جديد لتخزين المنتجات
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    price NUMERIC(10, 2)
);
```
لا تقلق بشأن فهم كل كلمة الآن، سنتناول كل هذه الأوامر بالتفصيل في الدروس القادمة.

---
