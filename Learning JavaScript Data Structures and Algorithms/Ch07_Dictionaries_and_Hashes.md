
# Ch07 Dictionaries and Hashes
<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

* [Ch07 Dictionaries and Hashes](#ch07-dictionaries-and-hashes)
  * [7.1 Dictionaries](#71-dictionaries)
  * [7.2 The hash table](#72-the-hash-table)
  * [7.3 Summary](#73-summary)

<!-- tocstop -->


## 7.1 Dictionaries

* Creating a dictionary


```python
# %load chapter07/01-Dictionaries.js
function Dictionary() {

  var items = {};

  this.set = function (key, value) {
    items[key] = value; //{1}
  };

  this.remove = function (key) {
    if (this.has(key)) {
      delete items[key];
      return true;
    }
    return false;
  };

  this.has = function (key) {
    return items.hasOwnProperty(key);
    //return value in items;
  };

  this.get = function (key) {
    return this.has(key) ? items[key] : undefined;
  };

  this.clear = function () {
    items = {};
  };

  this.size = function () {
    return Object.keys(items).length;
  };

  this.keys = function () {
    return Object.keys(items);
  };

  this.values = function () {
    var values = [];
    for (var k in items) {
      if (this.has(k)) {
        values.push(items[k]);
      }
    }
    return values;
  };

  this.each = function (fn) {
    for (var k in items) {
      if (this.has(k)) {
        fn(k, items[k]);
      }
    }
  };

  this.getItems = function () {
    return items;
  }
}

```

* Using the Dictionary class


```python
# %load chapter07/02-UsingDictionaries.js
var dictionary = new Dictionary();

dictionary.set('Gandalf', 'gandalf@email.com');
dictionary.set('John', 'johnsnow@email.com');
dictionary.set('Tyrion', 'tyrion@email.com');

console.log(dictionary.has('Gandalf'));   //outputs true
console.log(dictionary.size());   //outputs 3

console.log(dictionary.keys()); //outputs ["Gandalf", "John", "Tyrion"]
console.log(dictionary.values()); //outputs ["gandalf@email.com", "johnsnow@email.com", "tyrion@email.com"]
console.log(dictionary.get('Tyrion')); //outputs tyrion@email.com

dictionary.remove('John');

console.log(dictionary.keys()); //outputs ["Gandalf", "Tyrion"]
console.log(dictionary.values()); //outputs ["gandalf@email.com", "tyrion@email.com"]

console.log(dictionary.getItems()); //Object {Gandalf: "gandalf@email.com", Tyrion: "tyrion@email.com"}
```

## 7.2 The hash table

* Creating a hash table


```python
# %load chapter07/03-HashTable.js
function HashTable() {

  var table = [];

  var loseloseHashCode = function (key) {
    var hash = 0;
    for (var i = 0; i < key.length; i++) {
      hash += key.charCodeAt(i);
    }
    return hash % 37;
  };

  var djb2HashCode = function (key) {
    var hash = 5381;
    for (var i = 0; i < key.length; i++) {
      hash = hash * 33 + key.charCodeAt(i);
    }
    return hash % 1013;
  };

  var hashCode = function (key) {
    return loseloseHashCode(key);
  };

  this.put = function (key, value) {
    var position = hashCode(key);
    console.log(position + ' - ' + key);
    table[position] = value;
  };

  this.get = function (key) {
    return table[hashCode(key)];
  };

  this.remove = function (key) {
    table[hashCode(key)] = undefined;
  };

  this.print = function () {
    for (var i = 0; i < table.length; ++i) {
      if (table[i] !== undefined) {
        console.log(i + ": " + table[i]);
      }
    }
  };
}

```

* Using the HashTable class


```python
# %load chapter07/04-UsingHash.js
var hash = new HashTable();

hash.put('Gandalf', 'gandalf@email.com');
hash.put('John', 'johnsnow@email.com');
hash.put('Tyrion', 'tyrion@email.com');
hash.put('Aaron', 'aaron@email.com');
hash.put('Donnie', 'donnie@email.com');
hash.put('Ana', 'ana@email.com');
hash.put('Jonathan', 'jonathan@email.com');
hash.put('Jamie', 'jamie@email.com');
hash.put('Sue', 'sue@email.com');
hash.put('Mindy', 'mindy@email.com');
hash.put('Paul', 'paul@email.com');
hash.put('Nathan', 'nathan@email.com');

console.log('**** Printing Hash **** ');

hash.print();

console.log('**** Get **** ');

console.log(hash.get('Gandalf'));
console.log(hash.get('Loiane'));

console.log('**** Remove **** ');

hash.remove('Gandalf');
console.log(hash.get('Gandalf'));
hash.print();
```

* Hash table versus hash set


```python
# %load chapter07/05-HashCollisionSeparateChaining.js
function HashTableSeparateChaining() {

  var table = [];

  var ValuePair = function (key, value) {
    this.key = key;
    this.value = value;

    this.toString = function () {
      return '[' + this.key + ' - ' + this.value + ']';
    }
  };

  var loseloseHashCode = function (key) {
    var hash = 0;
    for (var i = 0; i < key.length; i++) {
      hash += key.charCodeAt(i);
    }
    return hash % 37;
  };

  var hashCode = function (key) {
    return loseloseHashCode(key);
  };

  this.put = function (key, value) {
    var position = hashCode(key);
    console.log(position + ' - ' + key);

    if (table[position] == undefined) {
      table[position] = new LinkedList();
    }
    table[position].append(new ValuePair(key, value));
  };

  this.get = function (key) {
    var position = hashCode(key);

    if (table[position] !== undefined && !table[position].isEmpty()) {

      //iterate linked list to find key/value
      var current = table[position].getHead();

      while (current.next) {
        if (current.element.key === key) {
          return current.element.value;
        }
        current = current.next;
      }

      //check in case first or last element
      if (current.element.key === key) {
        return current.element.value;
      }
    }
    return undefined;
  };

  this.remove = function (key) {

    var position = hashCode(key);

    if (table[position] !== undefined) {

      //iterate linked list to find key/value
      var current = table[position].getHead();

      while (current.next) {
        if (current.element.key === key) {
          table[position].remove(current.element);
          if (table[position].isEmpty()) {
            table[position] = undefined;
          }
          return true;
        }
        current = current.next;
      }

      //check in case first or last element
      if (current.element.key === key) {
        table[position].remove(current.element);
        if (table[position].isEmpty()) {
          table[position] = undefined;
        }
        return true;
      }
    }

    return false;
  };

  this.print = function () {
    for (var i = 0; i < table.length; ++i) {
      if (table[i] !== undefined) {
        console.log(table[i].toString());
      }
    }
  };
}

```

* Handling collisions between hash tables


```python
# %load chapter07/06-UsingHashCollisionSeparateChaining.js
var hashTableSeparateChaining = new HashTableSeparateChaining();

hashTableSeparateChaining.put('Gandalf', 'gandalf@email.com');
hashTableSeparateChaining.put('John', 'johnsnow@email.com');
hashTableSeparateChaining.put('Tyrion', 'tyrion@email.com');
hashTableSeparateChaining.put('Aaron', 'aaron@email.com');
hashTableSeparateChaining.put('Donnie', 'donnie@email.com');
hashTableSeparateChaining.put('Ana', 'ana@email.com');
hashTableSeparateChaining.put('Jonathan', 'jonathan@email.com');
hashTableSeparateChaining.put('Jamie', 'jamie@email.com');
hashTableSeparateChaining.put('Sue', 'sue@email.com');
hashTableSeparateChaining.put('Mindy', 'mindy@email.com');
hashTableSeparateChaining.put('Paul', 'paul@email.com');
hashTableSeparateChaining.put('Nathan', 'nathan@email.com');

console.log('**** Printing Hash **** ');

hashTableSeparateChaining.print();

console.log('**** Get **** ');

console.log(hashTableSeparateChaining.get('Jamie'));
console.log(hashTableSeparateChaining.get('Sue'));
console.log(hashTableSeparateChaining.get('Jonathan'));
console.log(hashTableSeparateChaining.get('Loiane'));

console.log('**** Remove **** ');

console.log(hashTableSeparateChaining.remove('Gandalf'));
console.log(hashTableSeparateChaining.get('Gandalf'));
hashTableSeparateChaining.print();

console.log(hashTableSeparateChaining.remove('Sue'));
hashTableSeparateChaining.print();

console.log(hashTableSeparateChaining.remove('Jamie'));
hashTableSeparateChaining.print();

console.log(hashTableSeparateChaining.remove('Donnie'));
hashTableSeparateChaining.print();
```


```python
# %load chapter07/07-HashCollisionLinearProbing.js
function HashLinearProbing() {

  var table = [];

  var ValuePair = function (key, value) {
    this.key = key;
    this.value = value;

    this.toString = function () {
      return '[' + this.key + ' - ' + this.value + ']';
    }
  };

  var loseloseHashCode = function (key) {
    var hash = 0;
    for (var i = 0; i < key.length; i++) {
      hash += key.charCodeAt(i);
    }
    return hash % 37;
  };

  var hashCode = function (key) {
    return loseloseHashCode(key);
  };

  this.put = function (key, value) {
    var position = hashCode(key);
    console.log(position + ' - ' + key);

    if (table[position] == undefined) {
      table[position] = new ValuePair(key, value);
    } else {
      var index = ++position;
      while (table[index] != undefined) {
        index++;
      }
      table[index] = new ValuePair(key, value);
    }
  };

  this.get = function (key) {
    var position = hashCode(key);

    if (table[position] !== undefined) {
      if (table[position].key === key) {
        return table[position].value;
      } else {
        var index = ++position;
        while (table[index] === undefined || table[index].key !== key) {
          index++;
        }
        if (table[index].key === key) {
          return table[index].value;
        }
      }
    }
    return undefined;
  };

  this.remove = function (key) {
    var position = hashCode(key);

    if (table[position] !== undefined) {
      if (table[position].key === key) {
        table[position] = undefined;
      } else {
        var index = ++position;
        while (table[index] === undefined || table[index].key !== key) {
          index++;
        }
        if (table[index].key === key) {
          table[index] = undefined;
        }
      }
    }
  };

  this.print = function () {
    for (var i = 0; i < table.length; ++i) {
      if (table[i] !== undefined) {
        console.log(i + ' -> ' + table[i].toString());
      }
    }
  };
}

```

* Creating better hash functions


```python
# %load chapter07/08-UsingHashCollisionLinearProbing.js
var hashLinearProbing = new HashLinearProbing();

hashLinearProbing.put('Gandalf', 'gandalf@email.com');
hashLinearProbing.put('John', 'johnsnow@email.com');
hashLinearProbing.put('Tyrion', 'tyrion@email.com');
hashLinearProbing.put('Aaron', 'aaron@email.com');
hashLinearProbing.put('Donnie', 'donnie@email.com');
hashLinearProbing.put('Ana', 'ana@email.com');
hashLinearProbing.put('Jonathan', 'jonathan@email.com');
hashLinearProbing.put('Jamie', 'jamie@email.com');
hashLinearProbing.put('Sue', 'sue@email.com');
hashLinearProbing.put('Mindy', 'mindy@email.com');
hashLinearProbing.put('Paul', 'paul@email.com');
hashLinearProbing.put('Nathan', 'nathan@email.com');

console.log('**** Printing Hash **** ');

hashLinearProbing.print();

console.log('**** Get **** ');

console.log(hashLinearProbing.get('Nathan'));
console.log(hashLinearProbing.get('Loiane'));

console.log('**** Remove **** ');

hashLinearProbing.remove('Gandalf');
console.log(hashLinearProbing.get('Gandalf'));
hashLinearProbing.print();
```

## 7.3 Summary

In this chapter, you learned about dictionaries, and how to add, remove, and get elements among other methods.
We also learned the difference between a dictionary and a set.
We also covered hashing, how to create a hash table (or hash map) data structure, how to add, remove, and get elements, and also how to create hash functions.
We learned how to handle collision in a hash table using two different techniques.
In the next chapter, we will learn a new data structure called a tree.




```python

```
