🧪 **4. تدريب: تسلسل الـ Promises**

قم بجلب بيانات JSON من واجهة برمجة التطبيقات (API) أدناه، واستخرج العنصر الأول، ثم اطبع خاصية `title` الخاصة به:
```javascript
fetch('[https://jsonplaceholder.typicode.com/todos](https://jsonplaceholder.typicode.com/todos)')
  .then(response => response.json())
  .then(data => {
    return data[0];
  })
  .then(firstItem => {
    console.log(firstItem.title);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```