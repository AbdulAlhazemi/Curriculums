🧪 **جرب بنفسك**
1.	استخدم `.find()` لتحديد مستخدم لديه `role: "admin"`:
    ```javascript
    const users = [
      { name: "Tom", role: "editor" },
      { name: "Lisa", role: "admin" },
      { name: "Jack", role: "subscriber" }
    ];

    // الناتج: { name: "Lisa", role: "admin" }
    ```
2.	استخدم `.some()` للتحقق مما إذا كان هناك أي رقم أقل من 10:
    ```javascript
    const values = [12, 18, 5, 20];

    // الناتج: true
    ```
3.	استخدم `.every()` لاختبار ما إذا كان جميع المستخدمين `verified` (متحقق منهم):
    ```javascript
    const users = [
      { name: "Anna", verified: true },
      { name: "Mike", verified: true },
      { name: "Sara", verified: false }
    ];

    // الناتج: false
    ```
