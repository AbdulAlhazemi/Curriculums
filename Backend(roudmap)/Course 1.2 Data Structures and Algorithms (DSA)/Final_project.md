## 🏆 المشروع النهائي: تطبيق هياكل البيانات والخوارزميات (مع تلميحات برمجية)

### 🎯 الهدف
الهدف من هذا المشروع هو ترسيخ فهمك لهياكل البيانات والخوارزميات عن طريق تطبيقها عمليًا. ستقوم ببناء الهياكل الأساسية بنفسك، ثم تستخدمها لحل مجموعة من التحديات البرمجية المعروفة.

---
### 📝 الجزء الأول: بناء هياكل البيانات من الصفر

#### 1. `LinkedList.js` (القائمة المرتبطة)
**المطلوب:** قائمة مرتبطة أحادية الاتجاه مع دوال `insert`, `delete`, `search`.
* **💡 تلميح برمجي:**
    ```javascript
    class Node {
      constructor(value) {
        this.value = value;
        this.next = null;
      }
    }

    class LinkedList {
      constructor() {
        this.head = null;
      }

      insert(value) {
        // ...
      }
    }
    ```

#### 2. `Stack.js` (المكدس)
**المطلوب:** مكدس مع دوال `push`, `pop`, `peek`.
* **💡 تلميح برمجي:**
    ```javascript
    class Stack {
      constructor() {
        this.items = [];
      }

      push(element) {
        // Use array's push method
      }

      pop() {
        // Use array's pop method
      }
    }
    ```

#### 3. `Queue.js` (الصف)
**المطلوب:** صف مع دوال `enqueue`, `dequeue`, `peek`.
* **💡 تلميح برمجي:**
    ```javascript
    class Queue {
      constructor() {
        this.items = [];
      }

      enqueue(element) {
        // Add to the end of the array
      }

      dequeue() {
        // Remove from the beginning of the array
      }
    }
    ```

#### 4. `BinarySearchTree.js` (شجرة البحث الثنائية)
**المطلوب:** شجرة بحث ثنائية مع دوال `insert` و `find`.
* **💡 تلميح برمجي:**
    ```javascript
    class Node {
        constructor(value) {
            this.value = value;
            this.left = null;
            this.right = null;
        }
    }

    class BinarySearchTree {
        constructor() {
            this.root = null;
        }

        insert(value) {
            const newNode = new Node(value);
            if (!this.root) {
                // ...
            } else {
                this.insertNode(this.root, newNode);
            }
        }

        insertNode(node, newNode) {
            // Recursive logic goes here
            // if (newNode.value < node.value) ...
        }
    }
    ```

#### 5. `Graph.js` (الرسم البياني)
**المطلوب:** رسم بياني (باستخدام قائمة المجاورة) مع دوال `addNode` و `addEdge`.
* **💡 تلميح برمجي:**
    ```javascript
    class Graph {
      constructor() {
        this.adjacencyList = {};
      }

      addNode(node) {
        if (!this.adjacencyList[node]) {
          this.adjacencyList[node] = [];
        }
      }

      addEdge(node1, node2) {
        // Add edge from node1 to node2
        // Add edge from node2 to node1 (for an undirected graph)
      }
    }
    ```
---
### 📝 الجزء الثاني: حل تحديات خوارزمية

#### 1. عكس سلسلة نصية (Reverse a String)
**المطلوب:** اكتب دالة تأخذ سلسلة نصية (`string`) وتعيدها معكوسة.
* **💡 تلميح برمجي:**
    ```javascript
    function reverseString(str) {
      // return str.split('')...
    }
    ```

#### 2. التحقق من الأقواس المتوازنة (Balanced Brackets)
**المطلوب:** اكتب دالة تتحقق مما إذا كانت الأقواس في سلسلة نصية متوازنة باستخدام **مكدس (Stack)**.
* **💡 تلميح برمجي:**
    ```javascript
    function isBalanced(str) {
      const stack = [];
      const map = {
        '(': ')',
        '[': ']',
        '{': '}'
      };

      for (let char of str) {
        if (map[char]) {
          // It's an opening bracket
          // ...
        } else {
          // It's a closing bracket
          const lastOpen = stack.pop();
          // ...
        }
      }
      return stack.length === 0;
    }
    ```

#### 3. إيجاد أقصر مسار في رسم بياني (Shortest Path)
**المطلوب:** استخدم الرسم البياني الذي بنيته، وطبق خوارزمية **البحث بالعرض أولاً (BFS)** لإيجاد أقصر مسار بين عقدتين.
* **💡 تلميح برمجي:**
    ```javascript
    function bfsShortestPath(graph, startNode, endNode) {
      const queue = [ [startNode] ]; // Queue stores paths
      const visited = new Set([startNode]);

      while (queue.length > 0) {
        const path = queue.shift();
        const node = path[path.length - 1];

        if (node === endNode) {
          return path;
        }

        for (let neighbor of graph.adjacencyList[node]) {
          // ...
        }
      }
    }
    ```

#### 4. فرز مصفوفة (Sorting)
**المطلوب:** قم بتطبيق خوارزمية **الفرز بالدمج (Merge Sort)**.
* **💡 تلميح برمجي:**
    ```javascript
    function mergeSort(arr) {
      // Base case
      if (arr.length <= 1) {
        return arr;
      }

      // Split the array
      const middle = Math.floor(arr.length / 2);
      const left = arr.slice(0, middle);
      const right = arr.slice(middle);

      // Recursive call and merge
      return merge(mergeSort(left), mergeSort(right));
    }

    function merge(left, right) {
      // Logic to merge two sorted arrays
    }
    ```