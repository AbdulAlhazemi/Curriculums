### 🛠️ تمرين عملي (Practice)

🧩 **المطلوب:**
1.  أنشئ وظيفة `canSwim` تضيف طريقة `swim()` إلى كائن.
2.  استخدم `composition` لإنشاء كائن `fish` يسبح فقط، و `duck` يسبح ويطير.

✍️ **نموذج البداية:**
```javascript
function canSwim(obj) {
  return {
    swim: () => console.log(`${obj.name} is swimming`)
  };
}

function createDuck(name) {
  const duck = { name };
  return {
    ...duck,
    ...canSwim(duck),
    fly: () => console.log(`${duck.name} is flying`)
  };
}
```
> 💡 **تلميح:** حاول التفكير في “القدرات” وليس “الأنواع” — هذا هو جوهر التركيب!

---
