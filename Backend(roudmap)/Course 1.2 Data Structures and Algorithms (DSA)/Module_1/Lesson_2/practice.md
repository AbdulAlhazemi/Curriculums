### 🧪 تدريب عملي

🔹 **المطلوب:**
احسب تعقيد الزمن (Time Complexity) للدالة التالية:

```javascript
function findSum(arr) {
  let sum = 0;
  for (let i = 0; i < arr.length; i++) { // تعمل n مرة
    for (let j = 0; j < arr.length; j++) { // تعمل n مرة
      sum += arr[i] + arr[j];
    }
  }
  return sum;
}
```
**الحل:** بما أن لدينا حلقة متداخلة, فإن عدد العمليات هو تقريبًا $n \times n = n^2$. إذن التعقيد هو $O(n^2)$.
