# الوحدة 4: البرمجة الشيئية في جافاسكريبت (OOP)

## الدرس 6: الوراثة في الأصناف (Classes)


🧠 **ماذا ستتعلم**
*	كيف تعمل وراثة الأصناف (class inheritance) في جافاسكريبت
*	استخدام `extends` لإنشاء أصناف فرعية (subclasses)
*	تجاوز الدوال (overriding methods) واستخدام `super`
*	فوائد الوراثة لإعادة استخدام الكود

---

🔍 **1. ما هي الوراثة؟**

الوراثة تسمح لصنف (الابن - child) بأن يرث خصائص ودوال من صنف آخر (الأب - parent)، مما يعزز إعادة استخدام الكود.

يمكن للصنف الابن إضافة وظائف أو تجاوزها.

---

👨‍💻 **2. إنشاء صنف فرعي (Subclass) باستخدام `extends`**
```javascript
class Vehicle {
  constructor(make) {
    this.make = make;
  }

  start() {
    console.log(`${this.make} is starting.`);
  }
}

class Car extends Vehicle {
  constructor(make, color) {
    super(make);  // استدعاء الدالة البانية للصنف الأب
    this.color = color;
  }

  drive() {
    console.log(`Driving a ${this.color} ${this.make}`);
  }
}

const myCar = new Car("Toyota", "red");
myCar.start(); // الناتج: Toyota is starting.
myCar.drive(); // الناتج: Driving a red Toyota
```

---

🔑 **3. استخدام `super`**
*	`super()` تستدعي الدالة البانية (constructor) للصنف الأب.
*	يمكنك أيضًا استدعاء دوال الصنف الأب باستخدام `super.methodName()`.

---

⚡ **4. تجاوز الدوال (Overriding Methods)**

يمكن للأصناف الأبناء تجاوز دوال الأصناف الآباء عن طريق تعريف دالة بنفس الاسم:
```javascript
class Car extends Vehicle { // بافتراض أن الصنف Vehicle معرّف كما في الأعلى
  start() {
    console.log(`Car ${this.make} is starting with a roar!`);
  }
}
```

---

🧠 **النقاط الرئيسية**
*	الوراثة تسمح للأصناف بمشاركة وتوسيع السلوك.
*	استخدم `extends` لإنشاء أصناف فرعية.
*	استدعِ `super()` لتشغيل الدالة البانية للصنف الأب.
*	قم بتجاوز الدوال لتخصيص سلوك الصنف الفرعي.

---