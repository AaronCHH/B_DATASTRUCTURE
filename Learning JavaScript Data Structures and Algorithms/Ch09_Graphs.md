
# Ch09 Graphs
<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

* [Ch09 Graphs](#ch09-graphs)
  * [9.1 Graph terminology](#91-graph-terminology)
  * [9.2 Representing a graph](#92-representing-a-graph)
  * [9.3 Creating the Graph class](#93-creating-the-graph-class)
  * [9.4 Graph traversals](#94-graph-traversals)
  * [9.5 Summary](#95-summary)

<!-- tocstop -->


## 9.1 Graph terminology

* Directed and undirected graphs

## 9.2 Representing a graph

* The adjacency matrix

* The adjacency list

* The incidence matrix

## 9.3 Creating the Graph class


```python
# %load chapter09/01-Graph.js
function Graph() {

    var vertices = []; //list

    var adjList = new Dictionary();

    this.addVertex = function(v){
        vertices.push(v);
        adjList.set(v, []); //initialize adjacency list with array as well;
    };

    this.addEdge = function(v, w){
        adjList.get(v).push(w);
        //adjList.get(w).push(v); //commented to run the improved DFS with topological sorting
    };

    this.toString = function(){
        var s = '';
        for (var i=0; i<vertices.length; i++){
            s += vertices[i] + ' -> ';
            var neighbors = adjList.get(vertices[i]);
            for (var j=0; j<neighbors.length; j++){
                s += neighbors[j] + ' ';
            }
            s += '\n';
        }
        return s;
    };

    var initializeColor = function(){
        var color = [];
        for (var i=0; i<vertices.length; i++){
            color[vertices[i]] = 'white';
        }
        return color;
    };

    this.bfs = function(v, callback){

        var color = initializeColor(),
            queue = new Queue();
        queue.enqueue(v);

        while (!queue.isEmpty()){
            var u = queue.dequeue(),
                neighbors = adjList.get(u);
            color[u] = 'grey';
            for (var i=0; i<neighbors.length; i++){
                var w = neighbors[i];
                if (color[w] === 'white'){
                    color[w] = 'grey';
                    queue.enqueue(w);
                }
            }
            color[u] = 'black';
            if (callback) {
                callback(u);
            }
        }
    };

    this.dfs = function(callback){

        var color = initializeColor();

        for (var i=0; i<vertices.length; i++){
            if (color[vertices[i]] === 'white'){
                dfsVisit(vertices[i], color, callback);
            }
        }
    };

    var dfsVisit = function(u, color, callback){

        color[u] = 'grey';
        if (callback) {
            callback(u);
        }
        console.log('Discovered ' + u);
        var neighbors = adjList.get(u);
        for (var i=0; i<neighbors.length; i++){
            var w = neighbors[i];
            if (color[w] === 'white'){
                dfsVisit(w, color, callback);
            }
        }
        color[u] = 'black';
        console.log('explored ' + u);
    };


    this.BFS = function(v){

        var color = initializeColor(),
            queue = new Queue(),
            d = [],
            pred = [];
        queue.enqueue(v);

        for (var i=0; i<vertices.length; i++){
            d[vertices[i]] = 0;
            pred[vertices[i]] = null;
        }

        while (!queue.isEmpty()){
            var u = queue.dequeue(),
                neighbors = adjList.get(u);
            color[u] = 'grey';
            for (i=0; i<neighbors.length; i++){
                var w = neighbors[i];
                if (color[w] === 'white'){
                    color[w] = 'grey';
                    d[w] = d[u] + 1;
                    pred[w] = u;
                    queue.enqueue(w);
                }
            }
            color[u] = 'black';
        }

        return {
            distances: d,
            predecessors: pred
        };
    };

    var time = 0;
    this.DFS = function(){

        var color = initializeColor(),
            d = [],
            f = [],
            p = [];
        time = 0;

        for (var i=0; i<vertices.length; i++){
            f[vertices[i]] = 0;
            d[vertices[i]] = 0;
            p[vertices[i]] = null;
        }

        for (i=0; i<vertices.length; i++){
            if (color[vertices[i]] === 'white'){
                DFSVisit(vertices[i], color, d, f, p);
            }
        }

        return {
            discovery: d,
            finished: f,
            predecessors: p
        };
    };

    var DFSVisit = function(u, color, d, f, p){

        console.log('discovered ' + u);
        color[u] = 'grey';
        d[u] = ++time;
        var neighbors = adjList.get(u);
        for (var i=0; i<neighbors.length; i++){
            var w = neighbors[i];
            if (color[w] === 'white'){
                p[w] = u;
                DFSVisit(w,color, d, f, p);
            }
        }
        color[u] = 'black';
        f[u] = ++time;
        console.log('explored ' + u);
    };
}
```

## 9.4 Graph traversals

* Breadth-first search (BFS)

* Depth-first search (DFS)


```python
# %load chapter09/02-UsingGraphs.js
var graph = new Graph();

var myVertices = ['A','B','C','D','E','F','G','H','I'];

for (var i=0; i<myVertices.length; i++){
    graph.addVertex(myVertices[i]);
}
graph.addEdge('A', 'B');
graph.addEdge('A', 'C');
graph.addEdge('A', 'D');
graph.addEdge('C', 'D');
graph.addEdge('C', 'G');
graph.addEdge('D', 'G');
graph.addEdge('D', 'H');
graph.addEdge('B', 'E');
graph.addEdge('B', 'F');
graph.addEdge('E', 'I');

console.log('********* printing graph ***********');

console.log(graph.toString());

console.log('********* bfs ***********');

function printNode(value){
    console.log('Visited vertex: ' + value);
}

graph.bfs(myVertices[0], printNode);

console.log('********* dfs ***********');

graph.dfs();

console.log('********* sorthest path - BFS ***********');
var shortestPathA = graph.BFS(myVertices[0]);
console.log(shortestPathA.distances);
console.log(shortestPathA.predecessors);

//from A to all other vertices
var fromVertex = myVertices[0];

for (i=1; i<myVertices.length; i++){
    var toVertex = myVertices[i],
        path = new Stack();
    for (var v=toVertex; v!== fromVertex; v=shortestPathA.predecessors[v]) {
        path.push(v);
    }
    path.push(fromVertex);
    var s = path.pop();
    while (!path.isEmpty()){
        s += ' - ' + path.pop();
    }
    console.log(s);
}

console.log('********* topological sort - DFS ***********');

//var result = graph.DFS();
//console.log(result.discovery);
//console.log(result.finished);
//console.log(result.predecessors);

graph = new Graph();

myVertices = ['A','B','C','D','E','F'];
for (i=0; i<myVertices.length; i++){
    graph.addVertex(myVertices[i]);
}
graph.addEdge('A', 'C');
graph.addEdge('A', 'D');
graph.addEdge('B', 'D');
graph.addEdge('B', 'E');
graph.addEdge('C', 'F');
graph.addEdge('F', 'E');


var result = graph.DFS();
console.log(result.discovery);
console.log(result.finished);
console.log(result.predecessors);

var fTimes = result.finished;
s = '';
for (var count=0; count<myVertices.length; count++){
    var max = 0;
    var maxName = null;
    for (i=0; i<myVertices.length; i++){
        if (fTimes[myVertices[i]] > max){
            max = fTimes[myVertices[i]];
            maxName = myVertices[i];
        }
    }
    s += ' - ' + maxName;
    delete fTimes[maxName];
}
console.log(s);

```

## 9.5 Summary

In this chapter, we covered the basic concepts of graphs.
We learned the different ways we can represent this data structure and we implemented an algorithm to represent a graph using adjacency list.
You also learned how to traverse a graph using BFS and DFS approaches.
This chapter also covered two applications of BFS and DFS, which are finding the shortest path using BFS and topological sorting using DFS.
In the next chapter, you will learn the most common sorting algorithms used in Computer Science.




```python

```
