🧪 **تحدي تدريبي**
1.	أنشئ مصفوفة `cars` تحتوي على 3 ماركات سيارات.
2.	قم بتغيير الماركة الثانية إلى شيء آخر.
3.	أضف ماركة جديدة إلى النهاية.
4.	قم بإزالة الماركة الأولى.
5.	اطبع المصفوفة النهائية وطولها.

تلميح:
```javascript
let cars = ["Toyota", "Ford", "BMW"];
cars[1] = "Tesla";
cars.push("Honda");
cars.shift();
console.log(cars);      // الناتج: ["Tesla", "BMW", "Honda"]
console.log(cars.length); // الناتج: 3
```