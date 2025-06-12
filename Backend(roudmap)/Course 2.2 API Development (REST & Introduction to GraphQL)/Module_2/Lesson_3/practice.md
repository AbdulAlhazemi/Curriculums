### 🛠️ تمرين عملي
1.  قم بتعديل المخطط (schema) لإضافة استعلام جديد اسمه `getDieRoll`. يجب أن يأخذ هذا الاستعلام معاملًا `numSides` من نوع `Int` ويُرجع `Int`.
    > تلميح المخطط: `getDieRoll(numSides: Int): Int`
2.  أضف دالة مُحلِّل مقابلة في الكائن `root`. يجب أن تُرجع هذه الدالة رقمًا عشوائيًا بين 1 و `numSides`.
    > تلميح الكود: `return Math.floor(Math.random() * numSides) + 1;`
3.  اختبر الاستعلام الجديد في GraphiQL. جرب إرسال استعلام مثل:
    ```graphql
    query {
      rollOne: getDieRoll(numSides: 6)
      rollTwo: getDieRoll(numSides: 20)
    }
    ```

---