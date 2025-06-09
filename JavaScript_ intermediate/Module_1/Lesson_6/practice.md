🧪 **تمرين صغير**

**المطلوب:**  
عند النقر على مهمة في القائمة، يجب أن يتم تمييزها كمكتملة باستخدام صنف CSS مثل `.completed`.

**الخطوات:**
1. أضف مستمع حدث `click` إلى كل عنصر `<li>`.
2. عند النقر، استخدم `classList.toggle("completed")` لتبديل حالة المهمة.

**مثال CSS:**
```css
.completed {
  text-decoration: line-through;
  color: gray;
}
```

**مساعدة:**
```javascript
li.addEventListener("click", () => {
  li.classList.toggle("completed");
});
```

---

## 🎯 التمرين 2: إضافة عداد للمهام المتبقية

**المطلوب:**  
أضف عنصر `<p>` أسفل قائمة المهام يعرض عدد المهام غير المكتملة.

**مثال:**  
> 📝 عدد المهام المتبقية: 2

**الخطوات:**
1. أضف عنصر `<p id="task-count">` في HTML.
2. أنشئ دالة `()updateCount` تحسب المهام غير المكتملة.
3. استدعِ هذه الدالة بعد كل إضافة أو حذف أو تغيير حالة مهمة.

**مساعدة:**
```javascript
function updateCount() {
  const tasks = taskList.querySelectorAll("li");
  const remaining = Array.from(tasks).filter(task => !task.classList.contains("completed")).length;
  document.getElementById("task-count").textContent = `عدد المهام المتبقية: ${remaining}`;
}
```

**تأكد من استدعاء `()updateCount` بعد:**
- إضافة مهمة
- حذف مهمة
- النقر على مهمة لتغيير حالتها

---

## 📌 أهداف هذه التمارين

- ربط DOM بحالة التطبيق الفعلية
- التعامل مع الأحداث والأنماط (CSS Classes)
- فهم أهمية تحديث الواجهة بناءً على البيانات
