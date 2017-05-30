
# Ch01 JavaScript - A Quick Overview
<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

* [Ch01 JavaScript - A Quick Overview](#ch01-javascript-a-quick-overview)
  * [1.1 Setting up the environment](#11-setting-up-the-environment)
  * [1.2 JavaScript basics](#12-javascript-basics)
  * [1.3 Control structures](#13-control-structures)
  * [1.4 Functions](#14-functions)
  * [1.5 Object-oriented programming](#15-object-oriented-programming)
  * [1.6 Debugging and tools](#16-debugging-and-tools)
  * [1.7 Summary](#17-summary)

<!-- tocstop -->


## 1.1 Setting up the environment

* The browser is enough

* Using web servers (XAMPP)

* It's all about JavaScript (Node.js)

## 1.2 JavaScript basics


```javascript
# %load chapter01/01-HelloWorld.js
function output(t) {
  document.write('<p>' + t + '</p>');
  return;
}

alert('Hello, World!');
console.log('Hello, World!');
output('Hello, World!');

```


```javascript
# %load chapter01/00-HelloWorld.html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <title>00</title>
</head>

<body>
  <script>
    alert('Hello World!');

  </script>
</body>

</html>

```


```javascript
# %load chapter01/01-HelloWorld.html
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title></title>
</head>

<body>
  <script type="text/javascript" src="01-HelloWorld.js"></script>
  <script type="text/javascript">
    /*alert('Hello, World!');
                console.log('Hello, World!');*/

  </script>
</body>

</html>

```

* Variables


```javascript
# %load chapter01/02-Variables.js
var num = 1; //{1}
num = 3; //{2}

var price = 1.5; //{3}
var name = 'Packt'; //{4}
var trueValue = true; //{5}
var nullVar = null; //{6}
var und;  //7

console.log("num: "+ num);
console.log("name: "+ name);
console.log("trueValue: "+ trueValue);
console.log("price: "+ price);
console.log("nullVar: "+ nullVar);
console.log("und: "+ und);

//******* Variable Scope

var myVariable = 'global';
myOtherVariable = 'global';

function myFunction(){
    var myVariable = 'local';
    return myVariable;
}

function myOtherFunction(){
    myOtherVariable = 'local';
    return myOtherVariable;
}

console.log(myVariable);   //{1}
console.log(myFunction()); //{2}

console.log(myOtherVariable);   //{3}
console.log(myOtherFunction()); //{4}
console.log(myOtherVariable);   //{5}

```


```javascript
# %load chapter01/02-Variables.html
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title></title>
</head>

<body>
  <script type="text/javascript" src="02-Variables.js"></script>
</body>

</html>

```

* Operators


```javascript
// # %load chapter01/03-Operators.js
/* Arithmetic operators */
var num = 0;
console.log('num value is ' + num);
```

    num value is 0





    undefined




```javascript
num = num + 2;
console.log('New num value is ' + num);
```

    New num value is 2





    undefined




```javascript
num = num * 3;
console.log('New num value is ' + num);
```

    New num value is 6





    undefined




```javascript
num = num / 2;
console.log('New num value is ' + num);
```

    New num value is 3





    undefined




```javascript
num++;
num--;
console.log('New num value is ' + num);
```

    New num value is 3





    undefined




```javascript
console.log('num mod 2 value is ' + (num % 2));
```

    num mod 2 value is 1





    undefined




```javascript
/* Assignment operators */
num += 1;
num -= 2;
num *= 3;
num /= 2;
num %= 3;

console.log('New num value is ' + num);
```

    New num value is 0





    undefined




```javascript
/* Assignment operators */
console.log('num == 1 : ' + (num == 1));
console.log('num === 1 : ' + (num === 1));
console.log('num != 1 : ' + (num != 1));
console.log('num > 1 : ' + (num > 1));
console.log('num < 1 : ' + (num < 1));
console.log('num >= 1 : ' + (num >= 1));
console.log('num <= 1 : ' + (num <= 1));
```

    num == 1 : false
    num === 1 : false
    num != 1 : true
    num > 1 : false
    num < 1 : true
    num >= 1 : false
    num <= 1 : true





    undefined




```javascript
/* Logical operators */
console.log('true && false : ' + (true && false));
console.log('true || false : ' + (true || false));
console.log('!true : ' + (!true));
```

    true && false : false
    true || false : true
    !true : false





    undefined




```javascript
/* Bitwise operators */
console.log('5 & 1:', (5 & 1)); //same as 0101 & 0001 (result 0001 / 1)
console.log('5 | 1:', (5 | 1)); //same as 0101 | 0001 (result 0101 / 5)
console.log('~ 5:', (~5)); //same as ~0101 (result 1010 / 10)
console.log('5 ^ 1:', (5 ^ 1)); //same as 0101 ^ 0001 (result 0100 / 4)
console.log('5 << 1:', (5 << 1)); //same as 0101 << 1 (result 1010 / 10)
console.log('5 >> 1:', (5 >> 1)); //same as 0101 >> 1 (result 0010 / 2)
```

    5 & 1: 1
    5 | 1: 5
    ~ 5: -6
    5 ^ 1: 4
    5 << 1: 10
    5 >> 1: 2





    undefined




```javascript
/* typeOf */
console.log('typeof num:', typeof num);
console.log('typeof Packt:', typeof 'Packt');
console.log('typeof true:', typeof true);
console.log('typeof [1,2,3]:', typeof [1,2,3]);
console.log('typeof {name:John}:', typeof {name:'John'});
```

    typeof num: number
    typeof Packt: string
    typeof true: boolean
    typeof [1,2,3]: object
    typeof {name:John}: object





    undefined




```javascript
/* delete */
var myObj = {name: 'John', age: 21};
delete myObj.age;
console.log(myObj); //Object {name: "John"}
```

    { name: 'John' }





    undefined



* Truthy and falsy


```javascript
// # %load chapter01/04-TruthyFalsy.js
function testTruthy(val) {
  return val ? console.log('truthy') : console.log('falsy');
}

testTruthy(true); //true
testTruthy(false); //false
testTruthy(new Boolean(false)); //true (object is always true)
```

    truthy
    falsy
    truthy





    undefined




```javascript
testTruthy(''); //false
testTruthy('Packt'); //true
testTruthy(new String('')); //true (object is always true)
```

    falsy
    truthy
    truthy





    undefined




```javascript
testTruthy(1); //true
testTruthy(-1); //true
testTruthy(NaN); //false
testTruthy(new Number(NaN)); //true (object is always true)
```

    truthy
    truthy
    falsy
    truthy





    undefined




```javascript
testTruthy({}); //true (object is always true)
```

    truthy





    undefined




```javascript
var obj = {
  name: 'John'
};
testTruthy(obj); //true
testTruthy(obj.name); //true
testTruthy(obj.age); //age (prop does not exist)
```

    truthy
    truthy
    falsy





    undefined



* The equals operators (== and ===)


```javascript
// # %load chapter01/05-EqualsOperators.js
//Packt == true

console.log('packt' ? true : false);
//outputs true
```

    true





    undefined




```javascript
console.log('packt' == true);
//1 - converts Boolean using toNumber
//'packt' == 1
//2 - converts String using toNumber
//NaN == 1
//outputs false
```

    false





    undefined




```javascript
console.log('packt' == false);
//1 - converts Boolean using toNumber
//'packt' == 0
//2 - converts String using toNumber
//NaN == 0
//outputs false
```

    false





    undefined




```javascript
console.log([0] == true);
//1 - converts Boolean using toNumber
//[0] == 1
//2 - converts Object using toPrimitive
//2.1 - [0].valueOf() is not primitive
//2.2 - [0].toString is 0
//0 == 1
//outputs false
```

    false





    undefined




```javascript
//******************************* ===
console.log('packt' === true); //false
```

    false





    undefined




```javascript
console.log('packt' === 'packt'); //true
```

    true





    undefined




```javascript
var person1 = {name:'John'};
var person2 = {name:'John'};
console.log(person1 === person2); //false, different objects
```

    false





    undefined



## 1.3 Control structures

* Conditional statements


```javascript
// # %load chapter01/06-ConditionalStatements.js
/* Example 01 - if */
var num = 1;
if (num === 1) {
  console.log("num is equal to 1");
}
```

    num is equal to 1





    undefined




```javascript
/* Example 02 - if-else */
var num = 0;
if (num === 1) {
  console.log("num is equal to 1");
} else {
  console.log("num is not equal to 1, the value of num is " + num);
}
```

    num is not equal to 1, the value of num is 0





    undefined




```javascript
/* Example 03 - if-else-if-else... */
var month = 5;
if (month === 1) {
  console.log("January");
} else if (month === 2) {
  console.log("February");
} else if (month === 3) {
  console.log("March");
} else {
  console.log("Month is not January, February or March");
}
```

    Month is not January, February or March





    undefined




```javascript
/* Example 04 - switch */
var month = 5;
switch (month) {
  case 1:
    console.log("January");
    break;
  case 2:
    console.log("February");
    break;
  case 3:
    console.log("March");
    break;
  default:
    console.log("Month is not January, February or March");
}
```

    Month is not January, February or March





    undefined




```javascript
/* Example 05 - ternary operator - if..else */
if (num === 1) {
  num--;
} else {
  num++;
}
```




    0




```javascript
//is the same as
(num === 1) ? num-- : num++;
```




    1



* Loops


```javascript
// # %load chapter01/07-Loops.js
console.log('**** for example ****');
```

    **** for example ****





    undefined




```javascript
/* for - example */
for (var i = 0; i < 10; i++) {
  console.log(i);
}
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
console.log('**** while example ****');
/* while - example */
var i = 0;
while (i < 10) {
  console.log(i);
  i++;
}
```

    **** while example ****
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





    9




```javascript
console.log('**** do-while example ****');
/* do-while - example */
var i = 0;
do {
  console.log(i);
  i++;
} while (i < 10)
```

    **** do-while example ****
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





    9



## 1.4 Functions


```javascript
// # %load chapter01/08-Functions.js
function sayHello() {
  console.log('Hello!');
}

sayHello();
```

    Hello!





    undefined




```javascript
/* function with parameter */
function output(text) {
  console.log(text);
}

output('Hello!');
```

    Hello!





    undefined




```javascript
output('Hello!', 'Other text');
```

    Hello!





    undefined




```javascript
output();
```

    undefined





    undefined




```javascript
/* function using the return statement */
function sum(num1, num2) {
  return num1 + num2;
}
```




    undefined




```javascript
var result = sum(1, 2);
output(result);
```

    3





    undefined



## 1.5 Object-oriented programming


```javascript
// # %load chapter01/09-ObjectOrientedJS.js
/* Object example 1 */

var obj = new Object();
```




    undefined




```javascript
/* Object example 2 */

var obj = {};
```




    undefined




```javascript
obj = {
  name: {
    first: 'Gandalf',
    last: 'the Grey'
  },
  address: 'Middle Earth'
};
```




    { name: { first: 'Gandalf', last: 'the Grey' },
      address: 'Middle Earth' }




```javascript
/* Object example 3 */

function Book(title, pages, isbn) {
  this.title = title;
  this.pages = pages;
  this.isbn = isbn;
  this.printIsbn = function () {
    console.log(this.isbn);
  }
}
```




    undefined




```javascript
var book = new Book('title', 'pag', 'isbn');
```




    undefined




```javascript
console.log(book.title); //outputs the book title
```

    title





    undefined




```javascript
book.title = 'new title'; //update the value of the book title
```




    'new title'




```javascript
console.log(book.title); //outputs the updated value
```

    new title





    undefined




```javascript
Book.prototype.printTitle = function () {
  console.log(this.title);
};
```




    [Function]




```javascript
book.printTitle();
```

    new title





    undefined




```javascript
book.printIsbn();
```

    isbn





    undefined



## 1.6 Debugging and tools

Both Firefox and Chrome support debugging.
A great tutorial from Google that shows you how to use Google Developer Tools to debug JavaScript can be found at https://developer.chrome.com/devtools/docs/javascript-debugging.
You can use any text editor of your preference.
But there are other great tools that can help you be more productive when working with JavaScript as well:

* Aptana: This is a free and open source IDE that supports JavaScript, CSS3, and HTML5, among other languages (http://www.aptana.com/).
* WebStorm: This is a very powerful JavaScript IDE with support for the latest web technologies and frameworks. It is a paid IDE, but you can download a 30-day trial version (http://www.jetbrains.com/webstorm/).
* Sublime Text: This is a lightweight text editor, and you can customize it by installing plugins. You can buy the license to support the development team, but you can also use it for free (the trial version does not expire) at http://www.sublimetext.com/.


## 1.7 Summary

In this chapter, we learned how to set up the development environment to be able to create or execute the examples in this book.
We also covered the basics of the JavaScript language that are needed prior to getting started with constructing the algorithms and data structures covered in this book.
In the next chapter, we will look at our first data structure, which is array, the most basic data structure that many languages support natively, including JavaScript.



```javascript

```
