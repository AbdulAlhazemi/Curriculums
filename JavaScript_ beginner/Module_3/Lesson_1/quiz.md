## ✅ اختبار قصير للتحقق (اختيار من متعدد)

### 1️⃣ ما الفرق بين تعريف الدالة (Function Declaration) وتعبير الدالة (Function Expression)؟

A. لا يوجد فرق بينهما  
B. تعريف الدالة يُخزن في متغير بينما التعبير لا  
C. تعريف الدالة يمكن استدعاؤه قبل تعريفه، بينما تعبير الدالة لا يمكن  
D. تعبير الدالة يُستخدم فقط مع الكائنات  

✅ **الإجابة الصحيحة:** C  
**تفسير:** تعريف الدالة يتم "رفعه" (hoisted) في JavaScript، بينما تعبير الدالة لا يُرفع.

---

### 2️⃣ هل يمكنك استدعاء تعبير دالة قبل تعريفه؟

A. نعم دائمًا  
B. فقط في المتصفحات الحديثة  
C. لا، يجب تعريفه أولًا  
D. نعم، إذا كانت داخل شرط `if`  

✅ **الإجابة الصحيحة:** C  
**تفسير:** تعبيرات الدوال لا تُرفع (hoisted)، لذلك يجب تعريفها قبل استخدامها.

---

### 3️⃣ ما هي الكلمة المفتاحية التي تُستخدم غالبًا لتخزين تعبيرات الدوال؟

A. `function`  
B. `const`  
C. `call`  
D. `define`  

✅ **الإجابة الصحيحة:** B  
**تفسير:** نستخدم غالبًا `const` لتخزين تعبيرات الدوال لجعلها غير قابلة لإعادة الإسناد (immutable).