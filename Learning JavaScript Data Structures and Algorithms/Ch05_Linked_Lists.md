
# Ch05 Linked Lists
<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

* [Ch05 Linked Lists](#ch05-linked-lists)
  * [5.1 Creating a linked list](#51-creating-a-linked-list)
  * [5.2 Doubly linked lists](#52-doubly-linked-lists)
  * [5.3 Circular linked lists](#53-circular-linked-lists)
  * [5.4 Summary](#54-summary)

<!-- tocstop -->


## 5.1 Creating a linked list


```python
# %load chapter05/01-Linked-List.js
function LinkedList() {

  var Node = function (element) {

    this.element = element;
    this.next = null;
  };

  var length = 0;
  var head = null;

  this.append = function (element) {

    var node = new Node(element),
      current;

    if (head === null) { //first node on list
      head = node;
    } else {

      current = head;

      //loop the list until find last item
      while (current.next) {
        current = current.next;
      }

      //get last item and assign next to added item to make the link
      current.next = node;
    }

    length++; //update size of list
  };

  this.insert = function (position, element) {

    //check for out-of-bounds values
    if (position >= 0 && position <= length) {

      var node = new Node(element),
        current = head,
        previous,
        index = 0;

      if (position === 0) { //add on first position

        node.next = current;
        head = node;

      } else {
        while (index++ < position) {
          previous = current;
          current = current.next;
        }
        node.next = current;
        previous.next = node;
      }

      length++; //update size of list

      return true;

    } else {
      return false;
    }
  };

  this.removeAt = function (position) {

    //check for out-of-bounds values
    if (position > -1 && position < length) {

      var current = head,
        previous,
        index = 0;

      //removing first item
      if (position === 0) {
        head = current.next;
      } else {

        while (index++ < position) {

          previous = current;
          current = current.next;
        }

        //link previous with current's next - skip it to remove
        previous.next = current.next;
      }

      length--;

      return current.element;

    } else {
      return null;
    }
  };

  this.remove = function (element) {

    var index = this.indexOf(element);
    return this.removeAt(index);
  };

  this.indexOf = function (element) {

    var current = head,
      index = 0;

    while (current) {
      if (element === current.element) {
        return index;
      }
      index++;
      current = current.next;
    }

    return -1;
  };

  this.isEmpty = function () {
    return length === 0;
  };

  this.size = function () {
    return length;
  };

  this.getHead = function () {
    return head;
  };

  this.toString = function () {

    var current = head,
      string = '';

    while (current) {
      string = current.element;
      current = current.next;
    }
    return string;

  };

  this.print = function () {
    console.log(this.toString());
  };
}

```

* Appending elements to the end of the linked list


```python
# %load chapter05/02-UsingLinkedLists.js
var list = new LinkedList();
list.append(15);
list.print();
console.log(list.indexOf(15));
list.append(10);
list.print();
console.log(list.indexOf(10));
list.append(13);
list.print();
console.log(list.indexOf(13));
console.log(list.indexOf(10));
list.append(11);
list.append(12);
list.print();
```

* Removing elements from the linked list


```python
console.log(list.removeAt(1));
list.print()
console.log(list.removeAt(3));
list.print();
list.append(14);
list.print();
```

* Inserting an element at any position


```python
list.insert(0,16);
list.print();
list.insert(1,17);
list.print();
list.insert(list.size(),18);
list.print();
```

* Implementing other methods


```python
list.remove(16);
list.print();
list.remove(11);
list.print();
list.remove(18);
list.print();
```

## 5.2 Doubly linked lists


```python
# %load chapter05/03-Doubly-Linked-List.js
function DoublyLinkedList() {

  var Node = function (element) {

    this.element = element;
    this.next = null;
    this.prev = null; //NEW
  };

  var length = 0;
  var head = null;
  var tail = null; //NEW

  this.append = function (element) {

    var node = new Node(element),
      current;

    if (head === null) { //first node on list
      head = node;
      tail = node; //NEW
    } else {

      //attach to the tail node //NEW
      tail.next = node;
      node.prev = tail;
      tail = node;
    }

    length++; //update size of list
  };

  this.insert = function (position, element) {

    //check for out-of-bounds values
    if (position >= 0 && position <= length) {

      var node = new Node(element),
        current = head,
        previous,
        index = 0;

      if (position === 0) { //add on first position

        if (!head) { //NEW
          head = node;
          tail = node;
        } else {
          node.next = current;
          current.prev = node; //NEW {1}
          head = node;
        }

      } else if (position === length) { //last item //NEW

        current = tail; // {2}
        current.next = node;
        node.prev = current;
        tail = node;

      } else {
        while (index++ < position) { //{3}
          previous = current;
          current = current.next;
        }
        node.next = current;
        previous.next = node;

        current.prev = node; //NEW
        node.prev = previous; //NEW
      }

      length++; //update size of list

      return true;

    } else {
      return false;
    }
  };

  this.removeAt = function (position) {

    //check for out-of-bounds values
    if (position > -1 && position < length) {

      var current = head,
        previous,
        index = 0;

      //removing first item
      if (position === 0) {

        head = current.next; // {1}

        //if there is only one item, then we update tail as well //NEW
        if (length === 1) { // {2}
          tail = null;
        } else {
          head.prev = null; // {3}
        }

      } else if (position === length - 1) { //last item //NEW

        current = tail; // {4}
        tail = current.prev;
        tail.next = null;

      } else {

        while (index++ < position) { // {5}

          previous = current;
          current = current.next;
        }

        //link previous with current's next - skip it to remove
        previous.next = current.next; // {6}
        current.next.prev = previous; //NEW
      }

      length--;

      return current.element;

    } else {
      return null;
    }
  };

  this.remove = function (element) {

    var index = this.indexOf(element);
    return this.removeAt(index);
  };

  this.indexOf = function (element) {

    var current = head,
      index = -1;

    //check first item
    if (element == current.element) {
      return 0;
    }

    index++;

    //check in the middle of the list
    while (current.next) {

      if (element == current.element) {
        return index;
      }

      current = current.next;
      index++;
    }

    //check last item
    if (element == current.element) {
      return index;
    }

    return -1;
  };

  this.isEmpty = function () {
    return length === 0;
  };

  this.size = function () {
    return length;
  };

  this.toString = function () {

    var current = head,
      s = current ? current.element : '';

    while (current && current.next) {
      current = current.next;
      s += ', ' + current.element;
    }

    return s;
  };

  this.inverseToString = function () {

    var current = tail,
      s = current ? current.element : '';

    while (current && current.prev) {
      current = current.prev;
      s += ', ' + current.element;
    }

    return s;
  };

  this.print = function () {
    console.log(this.toString());
  };

  this.printInverse = function () {
    console.log(this.inverseToString());
  };

  this.getHead = function () {
    return head;
  };

  this.getTail = function () {
    return tail;
  }
}

```

* Inserting a new element at any position


```python
# %load chapter05/04-UsingDoublyLinkedLists.js
var list = new DoublyLinkedList();

list.append(15);
list.print();
list.printInverse();

list.append(16);
list.print();
list.printInverse();

list.append(17);
list.print();
list.printInverse();

list.insert(0, 13);
list.print();
list.printInverse();

list.insert(4, 18);
list.print();
list.printInverse();

list.insert(1, 14);
list.print();
list.printInverse();
```

* Removing elements from any position


```python
list.removeAt(0);
list.print();
list.printInverse();

list.removeAt(list.size() - 1);
list.print();
list.printInverse();

list.removeAt(1);
list.print();
list.printInverse();

list.remove(16);
list.print();
list.printInverse();

list.remove(14);
list.print();
list.printInverse();

list.remove(17);
list.print();
list.printInverse();
```

## 5.3 Circular linked lists


```python
# %load chapter05/05-CircularLinkedList.js
function CircularLinkedList() {

  var Node = function (element) {

    this.element = element;
    this.next = null;
  };

  var length = 0;
  var head = null;

  this.append = function (element) {

    var node = new Node(element),
      current;

    if (head === null) { //first node on list
      head = node;
    } else {

      current = head;

      //loop the list until find last item
      while (current.next !== head) { //last element will be head instead of NULL
        current = current.next;
      }

      //get last item and assign next to added item to make the link
      current.next = node;
    }

    //set node.next to head - to have circular list
    node.next = head;

    length++; //update size of list
  };

  this.insert = function (position, element) {

    //check for out-of-bounds values
    if (position >= 0 && position <= length) {

      var node = new Node(element),
        current = head,
        previous,
        index = 0;

      if (position === 0) { //add on first position

        node.next = current;

        //update last element
        while (current.next !== head) { //last element will be head instead of NULL
          current = current.next;
        }

        head = node;
        current.next = head;

      } else {
        while (index++ < position) {
          previous = current;
          current = current.next;
        }
        node.next = current;
        previous.next = node;

        if (node.next === null) { //update in case last element
          node.next = head;
        }
      }

      length++; //update size of list

      return true;

    } else {
      return false;
    }
  };

  this.removeAt = function (position) {

    //check for out-of-bounds values
    if (position > -1 && position < length) {

      var current = head,
        previous,
        index = 0;

      //removing first item
      if (position === 0) {

        while (current.next !== head) { //needs to update last element first
          current = current.next;
        }

        head = head.next;
        current.next = head;

      } else { //no need to update last element for circular list

        while (index++ < position) {

          previous = current;
          current = current.next;
        }

        //link previous with current's next - skip it to remove
        previous.next = current.next;
      }

      length--;

      return current.element;

    } else {
      return null;
    }
  };

  this.remove = function (element) {

    var index = this.indexOf(element);
    return this.removeAt(index);
  };

  this.indexOf = function (element) {

    var current = head,
      index = -1;

    //check first item
    if (element == current.element) {
      return 0;
    }

    index++;

    //check in the middle of the list
    while (current.next !== head) {

      if (element == current.element) {
        return index;
      }

      current = current.next;
      index++;
    }

    //check last item
    if (element == current.element) {
      return index;
    }

    return -1;
  };

  this.isEmpty = function () {
    return length === 0;
  };

  this.size = function () {
    return length;
  };

  this.getHead = function () {
    return head;
  };

  this.toString = function () {

    var current = head,
      s = current.element;

    while (current.next !== head) {
      current = current.next;
      s += ', ' + current.element;
    }

    return s.toString();
  };

  this.print = function () {
    console.log(this.toString());
  };
}

```


```python
# %load chapter05/06-UsingCircularLinkedList.js
var circularLinkedList = new CircularLinkedList();

circularLinkedList.append(15);
circularLinkedList.print();

circularLinkedList.append(16);
circularLinkedList.print();

circularLinkedList.insert(0, 14);
circularLinkedList.print();

circularLinkedList.insert(1, 14.5);
circularLinkedList.print();

circularLinkedList.insert(4, 17);
circularLinkedList.print();

circularLinkedList.removeAt(0);
circularLinkedList.print();

circularLinkedList.removeAt(1);
circularLinkedList.print();

circularLinkedList.removeAt(2);
circularLinkedList.print();

console.log(circularLinkedList.indexOf(14.5));
console.log(circularLinkedList.indexOf(16));

```

## 5.4 Summary

In this chapter, you learned about the linked list data structure and its variants, the doubly linked list and the circular linked list.
You learned how to remove and add elements at any position and how to iterate through a linked list.
You also learned that the most important advantage of a linked list over an array is that you can easily add and remove elements from a linked list without shifting over its elements.
So, whenever you need to add and remove lots of elements, the best option would be a linked list instead of an array.
In the next chapter, you will learn about sets, the last sequential data structure that we will cover in this book.




```python

```
