## 📐 الوحدة 1: مبادئ الكود النظيف وأنماط التصميم

### 📘 الدرس 7: الأنماط السلوكية الشائعة (Common Behavioral Patterns)

#### 🧠 **ماذا ستتعلم**
* ما هي الأنماط السلوكية والغرض منها.
* كيف يسمح نمط المراقب (Observer) للكائنات بالاشتراك في الأحداث واستلام الإشعارات.
* كيف يمكّنك نمط الاستراتيجية (Strategy) من تبديل الخوارزميات في وقت التشغيل.
* كيف يوفر نمط الوسيط (Middleware) سلسلة من المعالجات لطلب معين.

---
### 🤔 1. ما هي الأنماط السلوكية؟
الأنماط السلوكية (Behavioral Patterns) هي الأنماط التي تهتم **بالخوارزميات وتوزيع المسؤوليات وأنماط التواصل بين الكائنات**. إذا كانت الأنماط الهيكلية هي "هيكل" التطبيق، فالأنماط السلوكية هي "ديناميكية" عمل هذا الهيكل.

---
### 👀 2. نمط المراقب (Observer)
**الهدف:** تعريف علاقة "واحد إلى كثير" بين الكائنات، بحيث عندما يغير كائن واحد (يُسمى **الموضوع Subject**) حالته، يتم إخطار جميع الكائنات المعتمدة عليه (تُسمى **المراقبين Observers**) وتحديثها تلقائيًا.

* **المشكلة التي يحلها:** لديك ناشر أخبار (الموضوع)، ولديك عدة مشتركين (المراقبون) يرغبون في الحصول على إشعار فوري عند نشر مقال جديد. لا تريد أن يكون الناشر مرتبطًا بشكل وثيق بكل مشترك.
> **ببساطة:** إنه مثل **الاشتراك في قناة يوتيوب**. عندما يقوم اليوتيوبر (الموضوع) برفع فيديو جديد، يحصل جميع المشتركين (المراقبون) على إشعار. اليوتيوبر لا يحتاج إلى معرفة هوية كل مشترك على حدة.

**مثال:**
```javascript
// الموضوع الذي تتم مراقبته
class NewsPublisher {
  constructor() { this.subscribers = []; }
  subscribe(subscriber) { this.subscribers.push(subscriber); }
  unsubscribe(subscriber) { /* ... منطق إلغاء الاشتراك ... */ }
  
  notify(news) {
    console.log(`Publisher: Publishing news -> ${news}`);
    this.subscribers.forEach(subscriber => subscriber.receiveNews(news));
  }
}
// المراقب الذي يستمع للتغييرات
class Subscriber {
  constructor(name) { this.name = name; }
  receiveNews(news) {
    console.log(`${this.name} received the news: "${news}"`);
  }
}

const publisher = new NewsPublisher();
const sub1 = new Subscriber('Ahmed');
const sub2 = new Subscriber('Sara');

publisher.subscribe(sub1);
publisher.subscribe(sub2);
publisher.notify('JavaScript course is now available!');
```

---
### ♟️ 3. نمط الاستراتيجية (Strategy)
**الهدف:** تعريف عائلة من الخوارزميات، وتغليف كل واحدة منها، وجعلها قابلة للتبديل.

* **المشكلة التي يحلها:** أنت تبني نظام شحن، ومنطق حساب تكلفة الشحن يختلف باختلاف الشركة (Aramex, FedEx, DHL). لا تريد كتابة كتلة `if/else if/else` ضخمة في الكود الرئيسي للتبديل بينها.
* **الحل:** تقوم بإنشاء "استراتيجية" منفصلة لكل خوارزمية حساب. الكود الرئيسي يختار الاستراتيجية التي يريد استخدامها في وقت التشغيل.
> **ببساطة:** تخطط لرحلة من الدمام إلى الرياض. يمكنك اختيار "استراتيجيتك": بالسيارة، بالقطار، أو بالطائرة. كل استراتيجية لها تكلفة ووقت مختلفان، لكن الهدف النهائي واحد. يمكنك التبديل بين الاستراتيجيات بسهولة.

**مثال:**
```javascript
// الاستراتيجيات المختلفة
class AramexShipping { calculate(pkg) { return pkg.weight * 5; } }
class FedExShipping { calculate(pkg) { return pkg.weight * 6; } }

// السياق الذي يستخدم الاستراتيجية
class ShippingCalculator {
  setStrategy(strategy) {
    this.strategy = strategy;
  }
  calculateCost(pkg) {
    return this.strategy.calculate(pkg);
  }
}

const calculator = new ShippingCalculator();
const pkg = { from: 'Dammam', to: 'Riyadh', weight: 2 };

calculator.setStrategy(new AramexShipping());
console.log(`Aramex cost: ${calculator.calculateCost(pkg)}`); // 10

calculator.setStrategy(new FedExShipping());
console.log(`FedEx cost: ${calculator.calculateCost(pkg)}`); // 12
```

---
### 🔗 4. نمط الوسيط (Middleware)
**الهدف:** إنشاء سلسلة من المعالجات لطلب معين. كل معالج يقرر إما معالجة الطلب وتمريره للمعالج التالي في السلسلة، أو إنهاء الدورة وإرسال استجابة.

* **المشكلة التي يحلها:** لديك طلب ويب وارد. قبل أن يصل إلى وجهته النهائية، تحتاج إلى القيام بسلسلة من الإجراءات: تسجيل الطلب (logging)، التحقق من الهوية (authentication)، التحقق من الصلاحيات (authorization)، إلخ.
> **ببساSطة:** إنه مثل **خط التجميع في مصنع**. المنتج يتحرك على حزام ناقل. المحطة الأولى تضيف قطعة، والثانية تطليه، والثالثة تفحصه. كل محطة يمكنها إما أن تؤدي عملها وتمرر المنتج للمحطة التالية، أو ترفضه وتوقف الخط.

**مثال:** هذا هو النمط الذي بني عليه إطار عمل Express.js بأكمله!
```javascript
// Middleware لتسجيل وقت الطلب
const requestTimeLogger = (req, res, next) => {
  req.requestTime = Date.now();
  console.log('Middleware 1: Logging time');
  next(); // مرر الطلب للمحطة التالية
};

// Middleware للتحقق من الهوية (مثال وهمي)
const fakeAuth = (req, res, next) => {
  console.log('Middleware 2: Checking auth');
  if (req.query.user === 'admin') {
    next(); // المستخدم مصرح له، مرر الطلب
  } else {
    res.status(401).send('Unauthorized'); // أوقف السلسلة وأرسل استجابة
  }
};

// استخدام السلسلة في مسار Express
app.get('/dashboard', requestTimeLogger, fakeAuth, (req, res) => {
  console.log('Final Handler: Reached dashboard');
  res.send('Welcome to the admin dashboard!');
});
```

---
