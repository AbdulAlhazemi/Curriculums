🧪 **تمرين صغير**

HTML:
```html
<ul id="tasks">
  <li>Learn HTML</li>
</ul>
```

JavaScript:
```javascript
let ul = document.getElementById("tasks");

let newTask = document.createElement("li");
newTask.textContent = "Learn DOM manipulation";

ul.appendChild(newTask);
```
