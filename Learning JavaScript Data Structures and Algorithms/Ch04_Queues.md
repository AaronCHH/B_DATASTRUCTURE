
# Ch04 Queues
<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

* [Ch04 Queues](#ch04-queues)
  * [4.1 Creating a queue](#41-creating-a-queue)
  * [4.2 The priority queue](#42-the-priority-queue)
  * [4.3 The circular queue Hot Potato](#43-the-circular-queue-hot-potato)
  * [4.4 Summary](#44-summary)

<!-- tocstop -->



## 4.1 Creating a queue

* The complete Queue class


```python
# %load chapter04/01-Queue.js
function Queue() {

    var items = [];

    this.enqueue = function(element){
        items.push(element);
    };

    this.dequeue = function(){
        return items.shift();
    };

    this.front = function(){
        return items[0];
    };

    this.isEmpty = function(){
        return items.length == 0;
    };

    this.clear = function(){
        items = [];
    };

    this.size = function(){
        return items.length;
    };

    this.print = function(){
        console.log(items.toString());
    };
}

```

* Using the Queue class


```python
# %load chapter04/02-UsingQueues.js
var queue = new Queue();
console.log(queue.isEmpty()); //outputs true

queue.enqueue("John");
queue.enqueue("Jack");
queue.print();

queue.enqueue("Camila");
queue.print();

console.log(queue.size()); //outputs 3
console.log(queue.isEmpty()); //outputs false

queue.dequeue();
queue.dequeue();
queue.print();

```

## 4.2 The priority queue


```python
# %load chapter04/03-PriorityQueue.js
function PriorityQueue() {

  var items = [];

  function QueueElement(element, priority) {
    this.element = element;
    this.priority = priority;
  }

  this.enqueue = function (element, priority) {
    var queueElement = new QueueElement(element, priority);

    if (this.isEmpty()) {
      items.push(queueElement);
    } else {
      var added = false;
      for (var i = 0; i < items.length; i++) {
        if (queueElement.priority < items[i].priority) {
          items.splice(i, 0, queueElement);
          added = true;
          break;
        }
      }
      if (!added) {
        items.push(queueElement);
      }
    }
  };

  this.dequeue = function () {
    return items.shift();
  };

  this.front = function () {
    return items[0];
  };

  this.isEmpty = function () {
    return items.length == 0;
  };

  this.size = function () {
    return items.length;
  };

  this.print = function () {
    for (var i = 0; i < items.length; i++) {
      console.log(items[i].element + ' - ' + items[i].priority);
    }
  };
}

var priorityQueue = new PriorityQueue();
priorityQueue.enqueue("John", 2);
priorityQueue.enqueue("Jack", 1);
priorityQueue.enqueue("Camila", 1);
priorityQueue.enqueue("Maxwell", 2);
priorityQueue.enqueue("Ana", 3);
priorityQueue.print();

```

## 4.3 The circular queue Hot Potato


```python
# %load chapter04/04-HotPotato.js
function hotPotato(nameList, num) {

  var queue = new Queue();

  for (var i = 0; i < nameList.length; i++) {
    queue.enqueue(nameList[i]);
  }

  var eliminated = '';
  while (queue.size() > 1) {
    for (var i = 0; i < num; i++) {
      queue.enqueue(queue.dequeue());
    }
    eliminated = queue.dequeue();
    console.log(eliminated + ' was eliminated from the Hot Potato game.');
  }

  return queue.dequeue();
}

var names = ['John', 'Jack', 'Camila', 'Ingrid', 'Carl'];
var winner = hotPotato(names, 7);
console.log('The winner is: ' + winner);

```

## 4.4 Summary

In this chapter, you learned about the queue data structure.
We implemented our own algorithm that represents a queue; you learned how to add and remove elements from it using the enqueue and dequeue methods.
We also covered two very famous special implementations of the queue: the priority queue and the circular queue (using the Hot Potato game implementation).
In the next chapter, you will learn about linked lists, a more complex data structure than the array.




```python

```
