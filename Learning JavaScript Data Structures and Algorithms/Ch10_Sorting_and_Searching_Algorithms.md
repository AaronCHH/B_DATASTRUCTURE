
# Ch10 Sorting and Searching Algorithms
<!-- TOC -->

- [Ch10 Sorting and Searching Algorithms](#ch10-sorting-and-searching-algorithms)
  - [10.1 Sorting algorithms](#101-sorting-algorithms)
  - [10.2 Searching algorithms](#102-searching-algorithms)
  - [10.3 Summary](#103-summary)

<!-- /TOC -->


## 10.1 Sorting algorithms


```python
# %load chapter10/01-SortingSearchingAlgorithms.js
function ArrayList(){

    var array = [];

    this.insert = function(item){
        array.push(item);
    };

    var swap = function(index1, index2){
        var aux = array[index1];
        array[index1] = array[index2];
        array[index2] = aux;
    };

    this.toString= function(){
        return array.join();
    };

    this.bubbleSort = function(){
        var length = array.length;

        for (var i=0; i<length; i++){
            console.log('--- ');
            for (var j=0; j<length-1; j++ ){
                console.log('compare ' + array[j] + ' with ' + array[j+1]);
                if (array[j] > array[j+1]){
                    console.log('swap ' + array[j] + ' with ' + array[j+1]);
                    swap(j, j+1);
                }
            }
        }
    };

    this.modifiedBubbleSort = function(){
        var length = array.length;

        for (var i=0; i<length; i++){
            console.log('--- ');
            for (var j=0; j<length-1-i; j++ ){
                console.log('compare ' + array[j] + ' with ' + array[j+1]);
                if (array[j] > array[j+1]){
                    console.log('swap ' + array[j] + ' with ' + array[j+1]);
                    swap(j, j+1);
                }
            }
        }

    };

    this.selectionSort = function(){
        var length = array.length,
            indexMin;

        for (var i=0; i<length-1; i++){
            indexMin = i;
            console.log('index ' + array[i]);
            for (var j=i; j<length; j++){
                if(array[indexMin]>array[j]){
                    console.log('new index min ' + array[j]);
                    indexMin = j;
                }
            }
            if (i !== indexMin){
                console.log('swap ' + array[i] + ' with ' + array[indexMin]);
                swap(i, indexMin);
            }
        }
    };

    this.insertionSort = function(){
        var length = array.length,
            j, temp;
        for (var i=1; i<length; i++){
            j = i;
            temp = array[i];
            console.log('to be inserted ' + temp);
            while (j>0 && array[j-1] > temp){
                console.log('shift ' + array[j-1]);
                array[j] = array[j-1];
                j--;
            }
            console.log('insert ' + temp);
            array[j] = temp;
        }
    };

    this.mergeSort = function(){
        array = mergeSortRec(array);
    };

    var mergeSortRec = function(array){

        var length = array.length;

        if(length === 1) {
            console.log(array);
            return array;
        }

        var mid = Math.floor(length / 2),
            left = array.slice(0, mid),
            right = array.slice(mid, length);

        return merge(mergeSortRec(left), mergeSortRec(right));
    };

    var merge = function(left, right){
        var result = [],
            il = 0,
            ir = 0;

        while(il < left.length && ir < right.length) {

            if(left[il] < right[ir]) {
                result.push(left[il++]);
            } else{
                result.push(right[ir++]);
            }
        }

        while (il < left.length){
            result.push(left[il++]);
        }

        while (ir < right.length){
            result.push(right[ir++]);
        }

        console.log(result);

        return result;
    };

    this.quickSort = function(){
        quick(array,  0, array.length - 1);
    };

    var partition = function(array, left, right) {

        var pivot = array[Math.floor((right + left) / 2)],
            i = left,
            j = right;

        console.log('pivot is ' + pivot + '; left is ' + left + '; right is ' + right);

        while (i <= j) {
            while (array[i] < pivot) {
                i++;
                console.log('i = ' + i);
            }

            while (array[j] > pivot) {
                j--;
                console.log('j = ' + j);
            }

            if (i <= j) {
                console.log('swap ' + array[i] + ' with ' + array[j]);
                swapQuickStort(array, i, j);
                i++;
                j--;
            }
        }

        return i;
    };

    var swapQuickStort = function(array, index1, index2){
        var aux = array[index1];
        array[index1] = array[index2];
        array[index2] = aux;
    };

    var quick = function(array, left, right){

        var index;

        if (array.length > 1) {

            index = partition(array, left, right);

            if (left < index - 1) {
                quick(array, left, index - 1);
            }

            if (index < right) {
                quick(array, index, right);
            }
        }
        return array;
    };

    this.sequentialSearch = function(item){

        for (var i=0; i<array.length; i++){
            if (item === array[i]){
                return i;
            }
        }

        return -1;
    };

    this.findMaxValue = function(){
        var max = array[0];
        for (var i=1; i<array.length; i++){
            if (max < array[i]){
                max = array[i];
            }
        }

        return max;
    };

    this.findMinValue = function(){
        var min = array[0];
        for (var i=1; i<array.length; i++){
            if (min > array[i]){
                min = array[i];
            }
        }

        return min;
    };

    this.binarySearch = function(item){
        this.quickSort();

        var low = 0,
            high = array.length - 1,
            mid, element;

        while (low <= high){
            mid = Math.floor((low + high) / 2);
            element = array[mid];
            console.log('mid element is ' + element);
            if (element < item) {
                low = mid + 1;
                console.log('low is ' + low);
            } else if (element > item) {
                high = mid - 1;
                console.log('high is ' + high);
            } else {
                console.log('found it');
                return mid;
            }
        }
        return -1;
    };

}
```


```python
# %load chapter10/02-UsingSortingAlgorithms.js
function createNonSortedArray(size){
    var array = new ArrayList();

    for (var i = size; i> 0; i--){
        array.insert(i);
    }

    return array;
}

function createRandomNonSortedArray(){
    var array = new ArrayList();

    array.insert(3);
    array.insert(5);
    array.insert(1);
    array.insert(4);
    array.insert(2);

    return array;
}
```

* Bubble sort


```python
console.log('********** Bubble Sort **********');

var array = createNonSortedArray(5);

console.log(array.toString());

array.bubbleSort();

console.log(array.toString());
```


```python
console.log('********** Modified Bubble Sort **********');

array = createNonSortedArray(5);

console.log(array.toString());

array.modifiedBubbleSort();

console.log(array.toString());
```

* Selection sort


```python
console.log('********** Selection Sort **********');

array = createNonSortedArray(5);

console.log(array.toString());

array.selectionSort();

console.log(array.toString());
```

* Insertion sort


```python
console.log('********** Insertion Sort **********');

array = createRandomNonSortedArray();

console.log(array.toString());

array.insertionSort();

console.log(array.toString());
```

* Merge sort


```python
console.log('********** Merge Sort **********');

array = createNonSortedArray(8);

console.log(array.toString());

array.mergeSort();

console.log(array.toString());
```

* Quick sort


```python
console.log('********** Quick Sort **********');
array = new ArrayList();

array.insert(3);
array.insert(5);
array.insert(1);
array.insert(6);
array.insert(4);
array.insert(7);
array.insert(2);

console.log(array.toString());

array.quickSort();

console.log(array.toString());
```

## 10.2 Searching algorithms


```python
# %load chapter10/03-UsingSearchingAlgorithms.js
function createNonSortedArray(items){
    var array = new ArrayList();

    for (var i = items; i> 0; i--){
        array.insert(i);
    }

    return array;
}

var array = createNonSortedArray(5);
```

* Sequential search


```python
console.log('********** Sequential Sort #3 **********');

console.log(array.sequentialSearch(3));
```


```python
console.log('********** Min **********');

console.log(array.findMinValue());
```


```python
console.log('********** Max **********');

console.log(array.findMaxValue());
```

* Binary search


```python
console.log('********** Binary Search #3 **********');

console.log(array.binarySearch(3));
```


```python
console.log('********** Binary Search #2 **********');

var array = createNonSortedArray(8);

console.log(array.binarySearch(2));
```

## 10.3 Summary


```python

```