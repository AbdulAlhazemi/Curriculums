# الوحدة 5: JSON والتعامل مع واجهات برمجة التطبيقات (APIs)

## الدرس 6: عرض بيانات API على الصفحة

🧠 **ماذا ستتعلم**
*	كيفية استخدام جافاسكريبت لعرض بيانات API ديناميكيًا على صفحة ويب
*	التعامل مع DOM لعرض البيانات المجتلبة
*	أفضل الممارسات لتحديث واجهة المستخدم (UI) باستجابات API

---

🔍 **1. لماذا نعرض بيانات API؟**

لا يكون جلب البيانات مفيدًا إلا إذا كان بإمكانك عرضها للمستخدمين. تسمح لك جافاسكريبت و DOM بإدراج المحتوى ديناميكيًا دون إعادة تحميل الصفحة.

---

👨‍💻 **2. مثال: عرض عناوين المهام (Todos)**

إليك مثال بسيط يجلب عناصر المهام ويعرضها في قائمة HTML:
```html
<ul id="todo-list"></ul>

<script>
async function loadTodos() {
  try {
    const response = await fetch('[https://jsonplaceholder.typicode.com/todos](https://jsonplaceholder.typicode.com/todos)');
    const todos = await response.json();

    const list = document.getElementById('todo-list');
    list.innerHTML = ''; // مسح المحتوى الحالي

    todos.slice(0, 5).forEach(todo => {
      const listItem = document.createElement('li');
      listItem.textContent = todo.title;
      list.appendChild(listItem);
    });
  } catch (error) {
    console.error('Failed to load todos:', error);
  }
}

loadTodos();
</script>
```

---

⚠️ **3. نصائح هامة**
*	قم دائمًا بمسح المحتوى السابق إذا كنت تقوم بتحديث عناصر موجودة (`innerHTML = ''`).
*	أنشئ عناصر DOM جديدة باستخدام `document.createElement()`.
*	ألحق العناصر الأبناء بالعناصر الآباء باستخدام `.appendChild()` أو `.append()`.
*	تعامل مع الأخطاء بلطف واعرض رسائل سهلة الاستخدام للمستخدم إذا لزم الأمر.

---

🧠 **النقاط الرئيسية**
*	استخدم دوال DOM لعرض بيانات API ديناميكيًا.
*	قم بمسح وتحديث المحتوى بعناية.
*	تعامل مع الأخطاء وقدم ملاحظات للمستخدمين.

---