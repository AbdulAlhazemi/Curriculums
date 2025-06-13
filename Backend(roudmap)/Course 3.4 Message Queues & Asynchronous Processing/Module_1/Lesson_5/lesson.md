## 📬 الوحدة 1: أساسيات طوابير الرسائل

### 📘 الدرس 5: تطبيق المنتج والمستهلك في Node.js

#### 🧠 **ماذا ستتعلم**
* كيفية استخدام مكتبة `amqplib` للاتصال بـ RabbitMQ.
* كيفية كتابة سكربت "منتج" (Producer) يرسل رسالة إلى تبادل.
* كيفية كتابة سكربت "مستهلك" (Consumer) يستمع لطابور ويعالج الرسائل.
* أهمية إقرار استلام الرسائل (Message Acknowledgement).

---
### 🧰 1. الأداة: مكتبة `amqplib`
`amqplib` هي مكتبة Node.js الأكثر شهرة وقوة للتفاعل مع RabbitMQ. هي تمنحنا دوال للتواصل مع وسيط الرسائل باستخدام بروتوكول AMQP.

**في بيئة التعلم الخاصة بنا:** هذه الحزمة مثبتة مسبقًا وجاهزة للاستخدام. كل ما عليك فعله هو استيرادها في الكود الخاص بك: `require('amqplib')`.

---
### 📤 2. كتابة المنتج (Producer)
المنتج هو البرنامج الذي يقوم بإنشاء الرسائل وإرسالها.

**الخطوات:**
1.  الاتصال بـ RabbitMQ.
2.  إنشاء قناة اتصال (Channel).
3.  التأكد من وجود التبادل (Exchange).
4.  نشر الرسالة إلى التبادل مع مفتاح توجيه.
5.  إغلاق الاتصال.

**مثال: `producer.js`**
```javascript
const amqp = require('amqplib');

async function send() {
  let connection;
  try {
    // 1. الاتصال بالخادم
    connection = await amqp.connect('amqp://localhost');
    
    // 2. إنشاء قناة
    const channel = await connection.createChannel();

    const exchange = 'my_direct_exchange';
    const routingKey = 'info';
    const message = 'Hello, RabbitMQ from a Node.js producer!';

    // 3. التأكد من وجود التبادل
    await channel.assertExchange(exchange, 'direct', { durable: false });

    // 4. نشر الرسالة
    channel.publish(exchange, routingKey, Buffer.from(message));
    
    console.log(`[x] Sent: '${message}'`);

  } catch (err) {
    console.error(err);
  } finally {
    if (connection) {
      // 5. إغلاق الاتصال بعد فترة قصيرة للسماح بإرسال الرسالة
      setTimeout(() => {
        connection.close();
        process.exit(0);
      }, 500);
    }
  }
}

send();
```

---
### 📥 3. كتابة المستهلك (Consumer)
المستهلك هو برنامج يعمل بشكل مستمر، يستمع إلى طابور معين، ويقوم بمعالجة الرسائل فور وصولها.

**الخطوات:**
1.  الاتصال بـ RabbitMQ وإنشاء قناة.
2.  التأكد من وجود نفس التبادل.
3.  إنشاء طابور.
4.  ربط الطابور بالتبادل باستخدام مفتاح التوجيه.
5.  البدء في استهلاك الرسائل من الطابور.
6.  **إرسال إقرار (ack)** بعد معالجة كل رسالة.

**مثال: `consumer.js`**
```javascript
const amqp = require('amqplib');

async function consume() {
  try {
    const connection = await amqp.connect('amqp://localhost');
    const channel = await connection.createChannel();

    const exchange = 'my_direct_exchange';
    const queue = 'info_queue';
    const routingKey = 'info';

    await channel.assertExchange(exchange, 'direct', { durable: false });
    await channel.assertQueue(queue, { durable: false });
    await channel.bindQueue(queue, exchange, routingKey);

    console.log(`[*] Waiting for messages in queue: ${queue}. To exit press CTRL+C`);

    channel.consume(queue, (msg) => {
      if (msg.content) {
        console.log(`[x] Received: ${msg.content.toString()}`);
        // 6. إرسال إقرار بأن الرسالة تمت معالجتها بنجاح
        // هذا يطلب من RabbitMQ حذف الرسالة من الطابور
        channel.ack(msg);
      }
    }, {
      noAck: false // يجب أن تكون false لضمان موثوقية المعالجة
    });

  } catch (err) {
    console.error(err);
  }
}

consume();
```
> **لماذا `channel.ack(msg)` مهمة؟** إذا توقف المستهلك عن العمل فجأة قبل إرسال `ack`، سيعرف RabbitMQ أن الرسالة لم تتم معالجتها وسيعيد إرسالها إلى مستهلك آخر. هذا يضمن عدم ضياع أي رسالة.

---
