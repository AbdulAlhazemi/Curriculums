🧪 **تحدي تدريبي**
1.	أنشئ كائنًا `student` يحتوي على `name` (الاسم)، `grade` (الدرجة)، و `id` (المعرف).
2.	قم بتحديث `grade` إلى `"A"`.
3.	أضف خاصية جديدة `enrolled` واضبط قيمتها على `true`.
4.	تحقق مما إذا كانت الخاصية `id` موجودة.
5.	اطبع الكائن النهائي.

تلميح:
```javascript
let student = {
  name: "Noah",
  grade: "B",
  id: 1234
};

student.grade = "A";
student.enrolled = true;
console.log("id" in student); // الناتج: true
console.log(student); // الناتج: { name: "Noah", grade: "A", id: 1234, enrolled: true }
```