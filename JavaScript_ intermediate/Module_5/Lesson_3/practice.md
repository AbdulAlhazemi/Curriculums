🧪 **4. تدريب: جلب وعرض البيانات**

حاول جلب البيانات من واجهة برمجة التطبيقات النموذجية أدناه واعرض خاصية `title` للعنصر الأول:
```javascript
fetch('[https://jsonplaceholder.typicode.com/todos](https://jsonplaceholder.typicode.com/todos)')
  .then(response => response.json())
  .then(data => {
    console.log(data[0].title);
  });
```