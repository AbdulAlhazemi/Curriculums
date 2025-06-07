🧪 **تمرين صغير**

HTML:
```html
<h1 id="welcome">Welcome!</h1>
<p class="info">This is a JavaScript lesson.</p>
```

JavaScript:
```javascript
let heading = document.querySelector("#welcome");
let info = document.querySelector(".info");

heading.textContent = "Hello DOM!";
info.style.color = "blue";
```
