
# Ch02 Arrays
<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

* [Ch02 Arrays](#ch02-arrays)
  * [2.1 Why should we use arrays?](#21-why-should-we-use-arrays)
  * [2.2 Creating and initializing arrays](#22-creating-and-initializing-arrays)
  * [2.3 Adding and removing elements](#23-adding-and-removing-elements)
  * [2.4 Two-dimensional and multi-dimensional arrays](#24-two-dimensional-and-multi-dimensional-arrays)
  * [2.5 References for JavaScript array methods](#25-references-for-javascript-array-methods)
    * [Note](#note)
  * [2.6 Summary](#26-summary)

<!-- tocstop -->


## 2.1 Why should we use arrays?


```javascript
// # %load chapter02/01-Introduction.js
var averageTempJan = 31.9;
var averageTempFeb = 35.3;
var averageTempMar = 42.4;
var averageTempApr = 52;
var averageTempMay = 60.8;
```




    undefined




```javascript
var averageTemp = [];
averageTemp[0] = 31.9;
averageTemp[1] = 35.3;
averageTemp[2] = 42.4;
averageTemp[3] = 52;
averageTemp[4] = 60.8;
```




    60.8



## 2.2 Creating and initializing arrays


```javascript
// # %load chapter02/02-CreatingAndInitialingArrays.js
var daysOfWeek = [];
```




    undefined




```javascript
var daysOfWeek = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
```




    undefined




```javascript
var daysOfWeek = new Array(); //{1}
```




    undefined




```javascript
var daysOfWeek = new Array(7); //{2}
```




    undefined




```javascript
console.log(daysOfWeek.length);
```

    7





    undefined




```javascript
var daysOfWeek = new Array('Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'); //{3}
```




    undefined




```javascript
for (var i = 0; i < daysOfWeek.length; i++) {
  console.log(daysOfWeek[i]);
}
```

    Sunday
    Monday
    Tuesday
    Wednesday
    Thursday
    Friday
    Saturday





    undefined




```javascript
//console.table(daysOfWeek);

//fibonacci numbers
// 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, ...
var fibonacci = []; //{1}
fibonacci[1] = 1; //{2}
fibonacci[2] = 1; //{3}
```




    1




```javascript
for (var i = 3; i < 20; i++) {
  fibonacci[i] = fibonacci[i - 1] + fibonacci[i - 2]; ////{4}
}
```




    4181




```javascript
for (var i = 1; i < fibonacci.length; i++) { //{5}
  console.log(fibonacci[i]); //{6}
}
```

    1
    1
    2
    3
    5
    8
    13
    21
    34
    55
    89
    144
    233
    377
    610
    987
    1597
    2584
    4181





    undefined




```javascript
//instead of {5} and {6} we can simply use
console.log(fibonacci);
```

    [ ,
      1,
      1,
      2,
      3,
      5,
      8,
      13,
      21,
      34,
      55,
      89,
      144,
      233,
      377,
      610,
      987,
      1597,
      2584,
      4181 ]





    undefined



## 2.3 Adding and removing elements


```javascript
// # %load chapter02/03-AddingRemovingElements.js
function printArray(myArray) {
  for (var i = 0; i < myArray.length; i++) {
    console.log(myArray[i]);
  }
}
```




    undefined




```javascript
var numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
printArray(numbers); // check
```

    0
    1
    2
    3
    4
    5
    6
    7
    8
    9





    undefined




```javascript
//
//**** add a new element to the numbers array
//
numbers[numbers.length] = 10;
```




    10




```javascript
numbers.push(11);
printArray(numbers); // check
```

    0
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11





    undefined




```javascript
numbers.push(12, 13);
printArray(numbers); // check
```

    0
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13





    undefined




```javascript
// *********************************
//insert first position manually
for (var i = numbers.length; i >= 0; i--) {
  numbers[i] = numbers[i - 1];
}
```




    undefined




```javascript
numbers[0] = -1;
printArray(numbers);
```

    -1
    0
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13





    undefined




```javascript
//using method unshift
numbers.unshift(-2);
printArray(numbers);
```

    -2
    -1
    0
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13





    undefined




```javascript
numbers.unshift(-4, -3);
printArray(numbers);
```

    -4
    -3
    -2
    -1
    0
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13





    undefined




```javascript
//
//**** Removing elements
//

numbers.pop();
```




    13




```javascript
//remove first position manually
for (var i = 0; i < numbers.length; i++) {
  numbers[i] = numbers[i + 1];
}
```




    undefined




```javascript
printArray(numbers);
```

    -3
    -2
    -1
    0
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    undefined





    undefined




```javascript
console.log(numbers.length);
```

    17





    undefined




```javascript
//using method shift
numbers.shift();
printArray(numbers);
```

    -2
    -1
    0
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    undefined





    undefined




```javascript
console.log(numbers.length);
```

    16





    undefined




```javascript
//**** Removing and Adding elements from the middle of the array or specific position
//splice method - parameter (index, howManyPositionsToBeRemoved, item1...itemX)
numbers.splice(5, 3);
console.log('----');
printArray(numbers);
```

    ----
    -2
    -1
    0
    1
    2
    6
    7
    8
    9
    10
    11
    12
    undefined





    undefined




```javascript
numbers.splice(5, 0, 2, 3, 4);
console.log('----');
printArray(numbers);
```

    ----
    -2
    -1
    0
    1
    2
    2
    3
    4
    6
    7
    8
    9
    10
    11
    12
    undefined





    undefined




```javascript
console.log('----');
numbers.splice(5, 3, 2, 3, 4);
printArray(numbers);
```

    ----
    -2
    -1
    0
    1
    2
    2
    3
    4
    6
    7
    8
    9
    10
    11
    12
    undefined





    undefined



## 2.4 Two-dimensional and multi-dimensional arrays


```javascript
// # %load chapter02/04-TwoDimensionalMultiDimensional.js
var averageTempDay1 = [72, 75, 79, 79, 81, 81];
var averageTempDay2 = [81, 79, 75, 75, 73, 72];

var averageTemp = [];
```




    undefined




```javascript
//same as
averageTemp[0] = [72, 75, 79, 79, 81, 81];
averageTemp[1] = [81, 79, 75, 75, 73, 72];
```




    [ 81, 79, 75, 75, 73, 72 ]




```javascript
function printMatrix(myMatrix) {
  for (var i = 0; i < myMatrix.length; i++) {
    for (var j = 0; j < myMatrix[i].length; j++) {
      console.log(myMatrix[i][j]);
    }
  }
}
```




    undefined




```javascript
printMatrix(averageTemp);
```

    72
    75
    79
    79
    81
    81
    81
    79
    75
    75
    73
    72





    undefined




```javascript
//same as

//day 1
averageTemp[0] = [];
averageTemp[0][0] = 72;
averageTemp[0][1] = 75;
averageTemp[0][2] = 79;
averageTemp[0][3] = 79;
averageTemp[0][4] = 81;
averageTemp[0][5] = 81;
```




    81




```javascript
//day 2
averageTemp[1] = [];
averageTemp[1][0] = 81;
averageTemp[1][1] = 79;
averageTemp[1][2] = 75;
averageTemp[1][3] = 75;
averageTemp[1][4] = 73;
averageTemp[1][5] = 72;
```




    72




```javascript
printMatrix(averageTemp);
```

    72
    75
    79
    79
    81
    81
    81
    79
    75
    75
    73
    72





    undefined




```javascript
//** Multidimensional Matrix

//Matrix 3x3x3 - Cube

var matrix3x3x3 = [];
for (var i = 0; i < 3; i++) {
  matrix3x3x3[i] = [];
  for (var j = 0; j < 3; j++) {
    matrix3x3x3[i][j] = [];
    for (var z = 0; z < 3; z++) {
      matrix3x3x3[i][j][z] = i + j + z;
    }
  }
}
```




    6




```javascript
for (var i = 0; i < matrix3x3x3.length; i++) {
  for (var j = 0; j < matrix3x3x3[i].length; j++) {
    for (var z = 0; z < matrix3x3x3[i][j].length; z++) {
      console.log(matrix3x3x3[i][j][z]);
    }
  }
}
```

    0
    1
    2
    1
    2
    3
    2
    3
    4
    1
    2
    3
    2
    3
    4
    3
    4
    5
    2
    3
    4
    3
    4
    5
    4
    5
    6





    undefined



## 2.5 References for JavaScript array methods

* Joining multiple arrays


```javascript
// # %load chapter02/05-ArrayMethods.js
//
//*** contact
//
var zero = 0;
var positiveNumbers = [1, 2, 3];
var negativeNumbers = [-3, -2, -1];
var numbers = negativeNumbers.concat(zero, positiveNumbers);

console.log(numbers);
```

    [ -3, -2, -1, 0, 1, 2, 3 ]





    undefined



* Iterator functions


```javascript
//
//*** every and some
//
var isEven = function (x) {
  // returns true if x is a multiple of 2.
  console.log(x);
  return (x % 2 == 0) ? true : false;
};
```




    undefined




```javascript
var numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15];

numbers.every(isEven); //is going to execute the function only once

console.log('---');
```

    1
    ---





    undefined




```javascript
numbers.some(isEven); //is going to execute the function twice

numbers.forEach(function (x) {
  console.log((x % 2 == 0));
});

console.log(numbers.reverse());
```

    1
    2
    false
    true
    false
    true
    false
    true
    false
    true
    false
    true
    false
    true
    false
    true
    false
    [ 15, 14, 13, 12, 11, 10, 9, 8, 7, 6, 5, 4, 3, 2, 1 ]





    undefined




```javascript
console.log('*** filter ***');
```

    *** filter ***





    undefined




```javascript
var evenNumbers = numbers.filter(isEven);
console.log(evenNumbers);
```

    15
    14
    13
    12
    11
    10
    9
    8
    7
    6
    5
    4
    3
    2
    1
    [ 14, 12, 10, 8, 6, 4, 2 ]





    undefined




```javascript
console.log('*** map ***');
```

    *** map ***





    undefined




```javascript
console.log(numbers.map(isEven));
```

    15
    14
    13
    12
    11
    10
    9
    8
    7
    6
    5
    4
    3
    2
    1
    [ false,
      true,
      false,
      true,
      false,
      true,
      false,
      true,
      false,
      true,
      false,
      true,
      false,
      true,
      false ]





    undefined




```javascript
console.log(numbers.reduce(function (previous, current, index) {
  return previous + current;
}));
```

    120





    undefined




```javascript
console.log(numbers.sort());
```

    [ 1, 10, 11, 12, 13, 14, 15, 2, 3, 4, 5, 6, 7, 8, 9 ]





    undefined



* Searching and sorting


```javascript
// ****
console.log(numbers.sort(function (a, b) {
  return a - b;
}));
```

    [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15 ]





    undefined




```javascript
function compare(a, b) {
  if (a < b) {
    return -1;
  }
  if (a > b) {
    return 1;
  }
  // a must be equal to b
  return 0;
}

console.log(numbers.sort(compare));
```

    [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15 ]





    undefined




```javascript
//Sorting objects

var friends = [
  {
    name: 'John',
    age: 30
  },
  {
    name: 'Ana',
    age: 20
  },
  {
    name: 'Chris',
    age: 25
  }
];
```




    undefined




```javascript
function comparePerson(a, b) {
  if (a.age < b.age) {
    return -1
  }
  if (a.age > b.age) {
    return 1
  }
  return 0;
}

console.log(friends.sort(comparePerson));
```

    [ { name: 'Ana', age: 20 },
      { name: 'Chris', age: 25 },
      { name: 'John', age: 30 } ]





    undefined




```javascript
var names = ['Ana', 'ana', 'john', 'John'];
console.log(names.sort());

console.log(names.sort(function (a, b) {
  if (a.toLowerCase() < b.toLowerCase()) {
    return -1
  }
  if (a.toLowerCase() > b.toLowerCase()) {
    return 1
  }
  return 0;
}));
```

    [ 'Ana', 'John', 'ana', 'john' ]
    [ 'Ana', 'ana', 'John', 'john' ]





    undefined




```javascript
var names2 = ['Maève', 'Maeve'];
console.log(names2.sort(function (a, b) {
  return a.localeCompare(b);
}));
```

    [ 'Maeve', 'Maève' ]





    undefined



* Outputting the array into a string


```javascript
//*** toString
console.log(numbers.toString());
```

    1,2,3,4,5,6,7,8,9,10,11,12,13,14,15





    undefined




```javascript
console.log(numbers.indexOf(10));
console.log(numbers.indexOf(100));
```

    9
    -1





    undefined




```javascript
numbers.push(10);
console.log(numbers.lastIndexOf(10));
console.log(numbers.lastIndexOf(100));
```

    15
    -1





    undefined




```javascript
var numbersString = numbers.join('-');
console.log(numbersString);
```

    1-2-3-4-5-6-7-8-9-10-11-12-13-14-15-10





    undefined



### Note
> There are some great resources that you can use to boost your knowledge about arrays and their methods:
* The first one is the arrays page from w3schools at http://www.w3schools.com/js/js_arrays.asp
* The second one is the array methods page from w3schools at http://www.w3schools.com/js/js_array_methods.asp
* Mozilla also has a great page about arrays and their methods with great examples at
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array (http://goo.gl/vu1diT)
* There are also great libraries that are very useful when working with arrays in JavaScript projects:
    * The Underscore library: http://underscorejs.org/
    * The Lo-Dash library: http://lodash.com/


## 2.6 Summary

In this chapter, we covered the most used data structure: arrays.
We learned how to declare, initialize, and assign values as well as add and remove elements.
We also learned about two-dimensional and multi-dimensional arrays as well as the main methods of an array, which will be very useful when we start creating our own algorithms in later chapters.
In the next chapter, we will learn about stacks, an array with a special behavior.



```javascript

```
