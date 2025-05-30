🧪 **تمرين صغير**

HTML:
```html
<ul id="pets">
  <li>Dog</li>
  <li>Cat</li>
  <li>Rabbit</li>
</ul>
```

JavaScript:
```javascript
let list = document.getElementById("pets");
let secondItem = list.children[1];

console.log(secondItem.textContent); // الناتج: "Cat"
console.log(secondItem.previousElementSibling.textContent); // الناتج: "Dog"
console.log(secondItem.nextElementSibling.textContent); // الناتج: "Rabbit"
```