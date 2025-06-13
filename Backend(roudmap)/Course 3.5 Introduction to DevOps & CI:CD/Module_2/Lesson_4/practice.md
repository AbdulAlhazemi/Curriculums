### 🛠️ تمرين عملي
1.  اذهب إلى إعدادات مستودعك على GitHub، ثم إلى `Secrets and variables` -> `Actions`.
2.  أنشئ **متغيرًا جديدًا** (`New repository variable`).
    * **Name:** `GREETING`
    * **Value:** `Hello from a GitHub variable!`
3.  عدّل ملف `ci.yml` الخاص بك. أضف خطوة جديدة في نهاية مهمة `test`.
    ```yaml
    - name: Print a custom message
      run: echo "${{ vars.GREETING }}"
    ```
4.  ادفع التغيير إلى مستودعك.
5.  اذهب إلى "Actions" وشاهد سجلات تشغيل سير العمل. يجب أن ترى رسالة الترحيب التي خزنتها في المتغير مطبوعة في السجل.

---