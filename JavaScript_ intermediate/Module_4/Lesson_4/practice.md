🧪 **4. تدريب: التحويل إلى صنف (Class)**

قم بتحويل هذه الدالة البانية إلى صنف ES6:
```javascript
function Book(title, author) {
  this.title = title;
  this.author = author;
}

Book.prototype.read = function() {
  console.log(`Reading ${this.title}`);
};
```