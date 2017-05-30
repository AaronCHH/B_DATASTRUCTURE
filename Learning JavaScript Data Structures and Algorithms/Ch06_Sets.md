
# Ch06 Sets
<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

* [Ch06 Sets](#ch06-sets)
  * [6.1 Creating a set](#61-creating-a-set)
  * [6.2 Set operations](#62-set-operations)
  * [6.3 Summary](#63-summary)

<!-- tocstop -->


## 6.1 Creating a set


```python
# %load chapter06/01-Set.js
/**
 * ECMSCRIPT 6 already have a Set class implementation:
 * https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set
 * We will try to copy  the same functionalities
 * @constructor
 */
function Set() {

  var items = {};

  this.add = function (value) {
    if (!this.has(value)) {
      items[value] = value;
      return true;
    }
    return false;
  };

  this.remove = function (value) {
    if (this.has(value)) {
      delete items[value];
      return true;
    }
    return false;
  };

  this.has = function (value) {
    return items.hasOwnProperty(value);
    //return value in items;
  };

  this.clear = function () {
    items = {};
  };

  /**
   * Modern browsers function
   * IE9+, FF4+, Chrome5+, Opera12+, Safari5+
   * @returns {Number}
   */
  this.size = function () {
    return Object.keys(items).length;
  };

  /**
   * cross browser compatibility - legacy browsers
   * for modern browsers use size function
   * @returns {number}
   */
  this.sizeLegacy = function () {
    var count = 0;
    for (var prop in items) {
      if (items.hasOwnProperty(prop))
        ++count;
    }
    return count;
  };

  /**
   * Modern browsers function
   * IE9+, FF4+, Chrome5+, Opera12+, Safari5+
   * @returns {Array}
   */
  this.values = function () {
    return Object.keys(items);
  };

  this.valuesLegacy = function () {
    var keys = [];
    for (var key in items) {
      keys.push(key);
    }
    return keys;
  };

  this.getItems = function () {
    return items;
  };

  this.union = function (otherSet) {
    var unionSet = new Set(); //{1}

    var values = this.values(); //{2}
    for (var i = 0; i < values.length; i++) {
      unionSet.add(values[i]);
    }

    values = otherSet.values(); //{3}
    for (var i = 0; i < values.length; i++) {
      unionSet.add(values[i]);
    }

    return unionSet;
  };

  this.intersection = function (otherSet) {
    var intersectionSet = new Set(); //{1}

    var values = this.values();
    for (var i = 0; i < values.length; i++) { //{2}
      if (otherSet.has(values[i])) { //{3}
        intersectionSet.add(values[i]); //{4}
      }
    }

    return intersectionSet;
  };

  this.difference = function (otherSet) {
    var differenceSet = new Set(); //{1}

    var values = this.values();
    for (var i = 0; i < values.length; i++) { //{2}
      if (!otherSet.has(values[i])) { //{3}
        differenceSet.add(values[i]); //{4}
      }
    }

    return differenceSet;
  };

  this.subset = function (otherSet) {

    if (this.size() > otherSet.size()) { //{1}
      return false;
    } else {
      var values = this.values();
      for (var i = 0; i < values.length; i++) { //{2}
        if (!otherSet.has(values[i])) { //{3}
          return false; //{4}
        }
      }
      return true;
    }
  };
}

```

* The has (value) method

* The add method

* The remove and clear methods

* The size method

* The values method

* Using the Set class


```python
# %load chapter06/02-UsingSets.js
var set = new Set();
```


```python
set.add(1);
console.log(set.values()); //outputs ["1"]
console.log(set.has(1));   //outputs true
console.log(set.size());   //outputs 1
```


```python
set.add(2);
console.log(set.values()); //outputs ["1", "2"]
console.log(set.has(2));   //true
console.log(set.size());   //2
console.log(set.sizeLegacy());   //3
```


```python
set.remove(1);
console.log(set.values()); //outputs ["2"]
```


```python
set.remove(2);
console.log(set.values()); //outputs []
```

## 6.2 Set operations

* Set union


```python
# %load chapter06/03-Operations.js
//--------- Union ----------

var setA = new Set();
setA.add(1);
setA.add(2);
setA.add(3);

var setB = new Set();
setB.add(3);
setB.add(4);
setB.add(5);
setB.add(6);

var unionAB = setA.union(setB);
console.log(unionAB.values());
```

* Set intersection


```python
//--------- Intersection ----------

var setA = new Set();
setA.add(1);
setA.add(2);
setA.add(3);

var setB = new Set();
setB.add(2);
setB.add(3);
setB.add(4);

var intersectionAB = setA.intersection(setB);
console.log(intersectionAB.values());
```

* Set difference


```python
//--------- Difference ----------

var setA = new Set();
setA.add(1);
setA.add(2);
setA.add(3);

var setB = new Set();
setB.add(2);
setB.add(3);
setB.add(4);

var differenceAB = setA.difference(setB);
console.log(differenceAB.values());
```

* Subset


```python
//--------- Subset ----------

var setA = new Set();
setA.add(1);
setA.add(2);

var setB = new Set();
setB.add(1);
setB.add(2);
setB.add(3);

var setC = new Set();
setC.add(2);
setC.add(3);
setC.add(4);

console.log(setA.subset(setB));
console.log(setA.subset(setC));
```

## 6.3 Summary

In this chapter, we learned how to implement a Set class from scratch, __which is similar to the Set class defined in the definition of ECMAScript 6__.
We also covered some methods that are not usually in other programming language implementations of the set data structure, such as union, intersection, difference, and subset.
So, we implemented a very complete Set class compared to the current implementation of Set in other programming languages.
In the next chapter, we will cover hashes and dictionaries, which are non sequential data structures.




```python

```
