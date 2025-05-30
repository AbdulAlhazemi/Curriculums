🧪 **تحدي تدريبي**
1.	أنشئ كائنًا `student` بخاصيتي `name` و `score`.
2.	أضف دالة `introduce` تطبع "Hi, I'm [name]".
3.	أضف دالة `addPoints` تزيد `score` بمقدار رقم معين.
4.	استدعِ كلتا الدالتين واطبع الكائن النهائي.

تلميح:
```javascript
let student = {
  name: "Maya",
  score: 85,
  introduce() {
    console.log("Hi, I'm " + this.name);
  },
  addPoints(points) {
    this.score += points;
  }
};

student.introduce();      // الناتج: "Hi, I'm Maya"
student.addPoints(10);
console.log(student.score); // الناتج: 95
```