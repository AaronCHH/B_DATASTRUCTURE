
# Ch03 Stacks
<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

* [Ch03 Stacks](#ch03-stacks)
  * [3.1 Creating a stack](#31-creating-a-stack)
  * [3.2 Decimal to binary](#32-decimal-to-binary)
  * [3.3 Summary](#33-summary)

<!-- tocstop -->



## 3.1 Creating a stack

* The complete Stack class


```javascript
// # %load chapter03/01-Stack.js
function Stack() {

  var items = [];

  this.push = function (element) {
    items.push(element);
  };

  this.pop = function () {
    return items.pop();
  };

  this.peek = function () {
    return items[items.length - 1];
  };

  this.isEmpty = function () {
    return items.length == 0;
  };

  this.size = function () {
    return items.length;
  };

  this.clear = function () {
    items = [];
  };

  this.print = function () {
    console.log(items.toString());
  };

  this.toString = function () {
    return items.toString();
  };
}

```




    undefined



* Using the Stack class


```javascript
// # %load chapter03/02-UsingStacks.js
var stack = new Stack();

console.log(stack.isEmpty()); //outputs true
```

    true





    undefined




```javascript
stack.push(5);
```




    undefined




```javascript
stack.push(8);
```




    undefined




```javascript
console.log(stack.peek()); // outputs 8
```

    8





    undefined




```javascript
stack.push(11);
```




    undefined




```javascript
console.log(stack.size()); // outputs 3
console.log(stack.isEmpty()); //outputs false
stack.push(15);
```

    3
    false





    undefined




```javascript
stack.pop();
```




    15




```javascript
stack.pop();
```




    11




```javascript
console.log(stack.size()); // outputs 2
```

    2





    undefined




```javascript
stack.print(); // outputs [5, 8]
```

    5,8





    undefined



## 3.2 Decimal to binary


```javascript
// # %load chapter03/04-DecimalToBinary.js
//233 == 11101001
//2x(10x10) + 3x(10) + 3x(1)

function divideBy2(decNumber) {

  var remStack = new Stack(),
    rem,
    binaryString = '';

  while (decNumber > 0) {
    rem = Math.floor(decNumber % 2);
    remStack.push(rem);
    decNumber = Math.floor(decNumber / 2);
  }

  while (!remStack.isEmpty()) {
    binaryString += remStack.pop().toString();
  }

  return binaryString;
}

console.log(divideBy2(233));
console.log(divideBy2(10));
console.log(divideBy2(1000));

/*
    The folow algorithm converts from base 10 to any base
 */
function baseConverter(decNumber, base) {

  var remStack = new Stack(),
    rem,
    baseString = '',
    digits = '0123456789ABCDEF';

  while (decNumber > 0) {
    rem = Math.floor(decNumber % base);
    remStack.push(rem);
    decNumber = Math.floor(decNumber / base);
  }

  while (!remStack.isEmpty()) {
    baseString += digits[remStack.pop()];
  }

  return baseString;
}

console.log(baseConverter(100345, 2));
console.log(baseConverter(100345, 8));
console.log(baseConverter(100345, 16));

```


```javascript
// # %load chapter03/05-TowerOfHanoi.js
function towerOfHanoi(n, from, to, helper) {

  if (n > 0) {
    towerOfHanoi(n - 1, from, helper, to);
    to.push(from.pop());
    console.log('-----')
    console.log('Source: ' + from.toString());
    console.log('Dest: ' + to.toString());
    console.log('Helper: ' + helper.toString());
    towerOfHanoi(n - 1, helper, to, from);
  }
}

var source = new Stack();
source.push(3);
source.push(2);
source.push(1);

var dest = new Stack();
var helper = new Stack();

towerOfHanoi(3, source, dest, helper);

source.print();
helper.print();
dest.print();

```

## 3.3 Summary

In this chapter, you learned about the stack data structure.
We implemented our own algorithm that represents a stack and you learned how to add and remove elements from it using the push and pop methods.
We also covered a very famous example of how to use a stack.
In the next chapter, you will learn about queues, which are very similar to stacks but use a different principle than LIFO.




```javascript

```
