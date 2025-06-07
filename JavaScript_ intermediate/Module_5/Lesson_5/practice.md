🧪 **4. تدريب: أعد كتابة `fetch` باستخدام `async/await`**

أعد كتابة سلسلة الـ `Promise` هذه باستخدام `async/await`:
```javascript
fetch('[https://jsonplaceholder.typicode.com/todos](https://jsonplaceholder.typicode.com/todos)')
  .then(response => response.json())
  .then(data => console.log(data[0].title))
  .catch(error => console.error(error));
```