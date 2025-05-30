🧪 **تحدي تدريبي**
1.	أنشئ كائنًا `movie` يحتوي على `title` (العنوان)، `year` (السنة)، و `rating` (التقييم).
2.	اطبع `title` باستخدام الترميز بالنقطة.
3.	قم بتغيير قيمة `rating` إلى قيمة جديدة.
4.	أضف خاصية جديدة تسمى `genre`.
5.	احذف خاصية `year` واطبع الكائن النهائي.

تلميح:
```javascript
let movie = {
  title: "Inception",
  year: 2010,
  rating: 8.8
};

console.log(movie.title); // الناتج: "Inception"
movie.rating = 9.0;
movie.genre = "Sci-Fi";
delete movie.year;

console.log(movie); // الناتج: { title: "Inception", rating: 9.0, genre: "Sci-Fi" }
```