🧪 **تحدي تدريبي**
1.	قم بالإعلان عن متغير عام `user = "Alice"`
2.	أنشئ دالة `changeUser()` تحتوي على متغير محلي يسمى أيضًا `user = "Bob"`
3.	داخل الدالة، اطبع `user`
4.	خارج الدالة، اطبع المتغير `user` العام

تلميح:
```javascript
let user = "Alice";

function changeUser() {
  let user = "Bob";
  console.log("Inside:", user); // الناتج: Bob
}

changeUser();
console.log("Outside:", user); // الناتج: Alice
```