## 📐 الوحدة 1: مبادئ الكود النظيف وأنماط التصميم

### 📘 الدرس 6: الأنماط الهيكلية الشائعة (Common Structural Patterns)

#### 🧠 **ماذا ستتعلم**
* ما هي الأنماط الهيكلية والغرض منها.
* كيف يسمح نمط المهايئ (Adapter) للواجهات غير المتوافقة بالعمل معًا.
* كيف يضيف نمط المزيّن (Decorator) وظائف جديدة لكائن ديناميكيًا.
* كيف يوفر نمط الواجهة (Facade) واجهة مبسطة لنظام معقد.
* تطبيق هذه الأنماط بأمثلة جافاسكريبت.

---
### 🤔 1. ما هي الأنماط الهيكلية؟
الأنماط الهيكلية (Structural Patterns) تهتم بكيفية **تجميع الكائنات والكلاسات لتكوين هياكل أكبر**، مع الحفاظ على مرونة وكفاءة هذه الهياكل. إذا كانت الأنماط الإنشائية تدور حول "تصنيع الأجزاء"، فإن الأنماط الهيكلية تدور حول "تجميع هذه الأجزاء معًا".

---
### 🔌 2. نمط المهايئ (Adapter)
**الهدف:** السماح لواجهات غير متوافقة بالعمل معًا.

* **المشكلة التي يحلها:** لديك كود قديم يتوقع التعامل مع كائن بواجهة معينة (مثل دالة `logMessage`)، ولكن لديك مكتبة جديدة رائعة توفر نفس الوظيفة ولكن بواجهة مختلفة (مثل دالة `log`). لا يمكنك تعديل الكود القديم ولا المكتبة الجديدة.
* **الحل:** تقوم بإنشاء "مهايئ" (Adapter) يعمل كوسيط يترجم الطلبات من الواجهة القديمة إلى الواجهة الجديدة.

> **ببساطة:** إنه مثل **محول قابس الكهرباء (power adapter)**. شاحن حاسوبك الأوروبي له رأسان دائريان، لكن مقبس الحائط في أمريكا له فتحتان مسطحتان. المحول يجلس في المنتصف، مما يسمح لهما بالعمل معًا دون تغيير أي منهما.

**مثال:**
```javascript
// المكتبة الجديدة التي لا يمكننا تعديلها
class NewLogger {
  log(data) { console.log(`New Logger says: ${data}`); }
}
// الكود القديم يتوقع وجود دالة logMessage
class LoggerAdapter {
  constructor() {
    this.newLogger = new NewLogger();
  }
  // المهايئ يوفر الواجهة القديمة
  logMessage(message) {
    // ولكنه داخليًا يستدعي الواجهة الجديدة
    this.newLogger.log(message);
  }
}

// الاستخدام
const logger = new LoggerAdapter();
logger.logMessage('Hello World!'); // يعمل بنجاح!
```
---
### 🎁 3. نمط المزيّن (Decorator)
**الهدف:** إضافة مسؤوليات أو وظائف جديدة إلى كائن بشكل ديناميكي.

* **المشكلة التي يحلها:** تخيل أن لديك كائن `Coffee`. تريد أن تكون قادرًا على إضافة "حليب" أو "سكر" إليه، مع تحديث السعر والوصف في كل مرة. إنشاء كلاس جديد لكل تركيبة ممكنة (`CoffeeWithMilk`, `CoffeeWithMilkAndSugar`, `CoffeeWithDoubleSugar`...) هو أمر غير عملي.
* **الحل:** تقوم بـ "تزيين" أو "تغليف" الكائن الأصلي بكائنات "مزينة" تضيف الوظيفة الجديدة.

> **ببساطة:** تطلب قهوة عادية، ثم "تزينها" بإضافة الحليب، ثم "تزين" المزيج الناتج بإضافة السكر. كل إضافة تغلف ما قبلها.

**مثال:**
```javascript
// الكائن الأساسي
class SimpleCoffee {
  getCost() { return 10; }
  getDescription() { return 'Simple coffee'; }
}

// المزيّنات
class MilkDecorator {
  constructor(coffee) { this.coffee = coffee; }
  getCost() { return this.coffee.getCost() + 2; }
  getDescription() { return this.coffee.getDescription() + ', milk'; }
}
class SugarDecorator {
  constructor(coffee) { this.coffee = coffee; }
  getCost() { return this.coffee.getCost() + 1; }
  getDescription() { return this.coffee.getDescription() + ', sugar'; }
}

// الاستخدام
let myCoffee = new SimpleCoffee();
myCoffee = new MilkDecorator(myCoffee); // نغلف القهوة بالحليب
myCoffee = new SugarDecorator(myCoffee); // نغلف المزيج بالسكر

console.log(myCoffee.getCost()); // 13 (10 + 2 + 1)
console.log(myCoffee.getDescription()); // Simple coffee, milk, sugar
```
---
### 🏛️ 4. نمط الواجهة (Facade)
**الهدف:** توفير واجهة بسيطة وموحدة لمجموعة من الواجهات في نظام فرعي معقد.

* **المشكلة التي يحلها:** لديك نظام معقد يتطلب عدة خطوات لتشغيله. على سبيل المثال، لتشغيل فيلم في نظام المسرح المنزلي، قد تحتاج إلى: تشغيل التلفاز، تشغيل مكبر الصوت، خفض الأضواء، تشغيل مشغل Blu-ray. هذه عملية معقدة ومتكررة.
* **الحل:** تقوم بإنشاء "واجهة" (Facade) بسيطة توفر دالة واحدة (مثل `watchMovie()`) تقوم بكل هذه الخطوات المعقدة نيابة عنك.

> **ببساطة:** إنه مثل زر **"مشاهدة فيلم"** على جهاز تحكم عن بعد عالمي. أنت تضغط على زر واحد، وهو يقوم بتنفيذ سلسلة من الأوامر المعقدة في الخلفية.

**مثال:**
```javascript
class TV { turnOn() { console.log('TV is ON'); } }
class SoundSystem { turnOn() { console.log('Sound System is ON'); } }
class Lights { dim() { console.log('Lights are dimmed'); } }

class HomeTheaterFacade {
  constructor(tv, sound, lights) {
    this.tv = tv;
    this.sound = sound;
    this.lights = lights;
  }
  watchMovie() {
    console.log('Get ready to watch a movie...');
    this.lights.dim();
    this.tv.turnOn();
    this.sound.turnOn();
  }
}

// الاستخدام
const facade = new HomeTheaterFacade(new TV(), new SoundSystem(), new Lights());
facade.watchMovie(); // كل شيء يتم بضغطة زر واحدة!
```
---

