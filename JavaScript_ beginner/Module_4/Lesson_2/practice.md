🧪 **تحدي تدريبي**
1.	أنشئ مصفوفة تحتوي على 5 من أفلامك المفضلة.
2.	استخدم `slice()` لنسخ الأفلام الثلاثة الوسطى.
3.	استخدم `splice()` لاستبدال الفيلم الأخير بفيلم جديد.
4.	استخدم `pop()` لإزالة العنصر الأخير وطباعة ما تم إزالته.
5.	اطبع المصفوفة النهائية.

تلميح:
```javascript
let movies = ["Inception", "Titanic", "Matrix", "Avatar", "Up"];
let middle = movies.slice(1, 4); // middle ستصبح ["Titanic", "Matrix", "Avatar"]
movies.splice(4, 1, "Interstellar"); // في الفهرس 4، أزل عنصرًا واحدًا، وأضف "Interstellar"
let removed = movies.pop();
console.log("Removed:", removed);
console.log("Final:", movies);
```