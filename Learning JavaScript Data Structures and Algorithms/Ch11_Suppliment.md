
# 第11章 演算法補充知識
<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

* [第11章 演算法補充知識](#第11章-演算法補充知識)
  * [11.1 遞迴](#111-遞迴)
  * [11.2 動態規劃](#112-動態規劃)
  * [11.3 食婪演算法](#113-食婪演算法)
  * [11.4 大O表示法](#114-大o表示法)
  * [11.5 從演算法實戰中獲得樂趣](#115-從演算法實戰中獲得樂趣)
  * [11.6 小結](#116-小結)

<!-- tocstop -->


## 11.1 遞迴

* JavaScript呼叫堆疊大小的限制

* 斐波那契數列


```python
# %load chapter11/01-Recursion.js
//Recursive solution - DP
function fibonacci(num){
    if (num === 1 || num === 2){
        return 1;
    }
    if (num > 2){
        return fibonacci(num - 1) + fibonacci(num - 2);
    }
}

//Non Recursive solution
function fib(num){
    var n1 = 1,
        n2 = 1,
        n = 1;
    for (var i = 3; i<=num; i++){
        n = n1 + n2;
        n1 = n2;
        n2 = n;
    }
    return n;
}

console.log(fibonacci(6));
console.log(fib(6));
```


```python
# %load chapter11/02-InfiniteRecursion.js
var i = 0;

function recursiveFn () {
    i++;
    recursiveFn();
}

try {
    recursiveFn();
} catch (ex) {
    alert('i = ' + i + ' error: ' + ex);
}

//chrome 37 = 20955 RangeError: Maximum call stack size exceeded
//ff 27 = 343429  InternalError: too much recursion
```

## 11.2 動態規劃

* 最少硬幣找零問題


```python
# %load chapter11/03-MinCoinChangeDP.js
function MinCoinChange(coins){

    var coins = coins;

    var cache = {};

    this.makeChange = function(amount) {
        var me = this;
        if (!amount) {
            return [];
        }
        if (cache[amount]) {
            return cache[amount];
        }
        var min = [], newMin, newAmount;
        for (var i=0; i<coins.length; i++){
            var coin = coins[i];
            newAmount = amount - coin;
            if (newAmount >= 0){
                newMin = me.makeChange(newAmount);
            }
            if (
                newAmount >= 0 &&
                (newMin.length < min.length-1 || !min.length) &&
                (newMin.length || !newAmount)
                ){
                min = [coin].concat(newMin);
                console.log('new Min ' + min + ' for ' + amount);
            }
        }
        return (cache[amount] = min);
    };
}


var minCoinChange = new MinCoinChange([1, 5, 10, 25]);
console.log(minCoinChange.makeChange(36));

var minCoinChange2 = new MinCoinChange([1, 3, 4]);
console.log(minCoinChange2.makeChange(6));
```

## 11.3 食婪演算法

* 最少硬幣找零問題


```python
# %load chapter11/04-MinCoinChangeGreedy.js
function MinCoinChange(coins){

    var coins = coins;

    var cache = {};

    this.makeChange = function(amount) {
        var change = [],
            total = 0;
        for (var i=coins.length; i>=0; i--){
            var coin = coins[i];
            while (total + coin <= amount) {
                change.push(coin);
                total += coin;
            }
        }
        return change;
    };
}


var minCoinChange = new MinCoinChange([1, 5, 10, 25]);
console.log(minCoinChange.makeChange(36));

var minCoinChange2 = new MinCoinChange([1, 3, 4]);
console.log(minCoinChange2.makeChange(6));
```

## 11.4 大O表示法


```python
# %load chapter11/bigOChart/chart.js
google.load('visualization', '1.0', {'packages':['corechart']});
google.setOnLoadCallback(drawChart);

function drawChart() {

    var data = new google.visualization.DataTable();
    data.addColumn('string', 'n');
    data.addColumn('number', 'O(1)');
    data.addColumn('number', 'O(log n)');
    data.addColumn('number', 'O(n)');
    data.addColumn('number', 'O(n log n)');
    data.addColumn('number', 'O(n^2)');
    data.addColumn('number', 'O(2^n)');

    for (var i = 0; i <= 30; i++) {
        data.addRow([i+'', 1, Math.log(i), i, Math.log(i)*i, Math.pow(i,2), Math.pow(2,i)]);
    }

    var options = {'title':'Big O Notation Complexity Chart',
        'width':700,
        'height':600,
        'backgroundColor':{stroke:'#CCC',strokeWidth:1},
        'curveType':'function',
        'hAxis':{
            title:'Elements (n)',
            showTextEvery:5
        },
        'vAxis':{
            title:'Operations',
            viewWindowMode:'explicit',
            viewWindow:{min:0,max:450}
        }
    };

    var chart = new google.visualization.LineChart(document.getElementById('chart_div'));
    chart.draw(data, options);
}
```

* 理解大O表示法

* 時間複雜度比較

## 11.5 從演算法實戰中獲得樂趣

## 11.6 小結


```python

```
