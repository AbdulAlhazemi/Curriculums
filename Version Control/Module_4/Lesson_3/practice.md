### 🧪 تمارين تدريبية (في المحرر)
1.  عدّل على ملف، ثم نفّذ `git add` و `commit`.
2.  لاحظ أن رسالة `commit` فيها خطأ إملائي.
3.  صحّح الرسالة باستخدام:
    ```bash
    git commit --amend -m "رسالة مصححة"
    ```
4.  في مشروع يحتوي على فرعين، نفّذ:
    ```bash
    git switch feature
    git rebase main
    ```
5.  لاحظ كيف أصبحت `commits` في `feature` فوق `main` باستخدام `git log`.
