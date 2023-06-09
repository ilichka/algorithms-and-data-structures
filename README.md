# Popular algorithms and data structures

## Here you can find following things:

1. Algorithms 
   - Search
   - Sort
   - Recursion
   - Dijkstra's
   - Tree traversal
   - Cashing
2. Structures
   - Arrays
   - Linked list
   - Queue
   - Set
   - Map
   - Binary tree
   - n-tree
   - Graphs

First of all lets understand for what purpose we need algorithms. All algorithms can be described
with `Big O` annotation. In `Big O` we always take the worst case.



#### sssssssssssssss

## Linear search

Initialize an array and create search function. Function accepts an array and element,
that we want to find. With `for` cycle iterate by array and return an index of element, that we found.
If no element - return null. Also, we count iterations.

```javascript
const array = [1,4,5,8,5,1,2,7,5,2,11]

let count = 0

function linearSearch(array, item) {
    for (let i = 0; i < array.length; i++) {
        count += 1
        if (array[i] === item) {
            return i;
        }
    }
    return null
}

console.log(linearSearch(array, 1))
console.log('count = ', count)
```

In fact the difficulty of this algorithm is `O(n)`.

## Binary search

To create this algorithm we can use recursion and cycle.

Steps of binary search:
1. Find center element
2. Create flag `found` and index `position`.
3. Create while cycle, which will work till we find element, or till our start and end
are equal.
4. Crete if statements:
   - if we found our item
   - if current element bigger than item
   - if current element less than item
5. Return element position

In case of recursion we have the same flow.

```javascript
const array = [0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15]
let count = 0

function binarySearch(array, item) {
    let start = 0
    let end = array.length
    let middle;
    let found = false
    let position = -1
    while (found === false && start <= end) {
        count+=1
        middle = Math.floor((start + end) / 2);
        if (array[middle] === item) {
            found = true
            position = middle
            return position;
        }
        if (item < array[middle]) {
            end = middle - 1
        } else {
            start = middle + 1
        }
    }
    return position;
}

function recursiveBinarySearchAlgorithm(array, item, start, end) {
    let middle = Math.floor((start + end) / 2);
    count += 1
    if (item === array[middle]) {
        return middle
    }
    if (item < array[middle]) {
        return recursiveBinarySearch(array, item, 0, middle - 1 )
    } else {
        return recursiveBinarySearch(array, item, middle + 1, end )
    }
}

const recursiveBinarySearch = (array, item) => {
    return recursiveBinarySearchAlgorithm(array, item, 0, array.length)
}

console.log(recursiveBinarySearch(array, 0))
console.log(count)
```

## Selection sort

Selection sort workflow: 
1. We have an unordered array
2. Find minimal element in an array 
3. Swap with first element
4. Then the same algorithm, but exclude already sorted elements

```javascript
const arr = [0,3,2,5,6,8,1,9,4,2,1,2,9,6,4,1,7,-1, -5, 23,6,2,35,6,3,32] // [0,1,1,2,3.......]
let count = 0

function selectionSort(array) {
    for (let i = 0; i < array.length; i++) {
        let indexMin = i
        for (let j = i+1; j < array.length; j++) {
            if (array[j] < array[indexMin]) {
                indexMin = j
            }
            count += 1
        }
        let tmp = array[i]
        array[i] = array[indexMin]
        array[indexMin] = tmp
    }
    return array
}

console.log(selectionSort(arr))
console.log(arr.length) // O(n*n)
console.log('count = ', count)
```

In fact difficulty will be here O(1/2n*n), but in `Big O` annotation we dont care about
this coefficients, so the difficulty is O(n^2).

## Bubble sort

The algorithm is simple. We iterate by an array and compares two nearby elements, if the next one is more than current -
just swap them.

```javascript
const arr = [0,3,2,5,6,8,23,9,4,2,1,2,9,6,4,1,7,-1, -5, 23,6,2,35,6,3,32,9,4,2,1,2,9,6,4,1,7,-1, -5, 23,9,4,2,1,2,9,6,4,1,7,-1, -5, 23,]
let count = 0

function bubbleSort(array) {
    for (let i = 0; i < array.length; i++) {
        for (let j = 0; j < array.length; j++) {
            if (array[j + 1] < array[j]) {
                let tmp = array[j]
                array[j] = array[j+1]
                array[j+1] = tmp
            }
            count+=1
        }
    }
    return array
}

console.log('length', arr.length)
console.log(bubbleSort(arr)) // O(n*n)
console.log('count = ', count)
```

Here we have pure difficulty O(n^2) without any coefficients. 

## Quick sort

Main concept there is divide adn concur. We divide array into 2 arrays and each time we 
select a "pivot" on each array. Iterate an array and all elements, that are less move to left,
other to right. Then do the same for each array. We will do it till the array length !== 1

Here we have difficulty O(log(n)*n)

## Recursion

Recursion is a function, that calls itself.

Examples: 

```javascript
const factorial = (n) => {
    if (n === 1) {
        return 1
    }
    return n * factorial(n - 1)
}

//  Fibonacci array -  1,1,2,3,5,8,13,21

const fibonacci = (n) => {
    if (n === 1 || n === 2) {
        return 1
    }
    return fibonacci(n-1) + fibonacci(n-2)
}

console.log(fibonacci(8))
```

## Graphs

Graph - a structure made of vertices and edges. Graph could be:
1. Directed

![](directed.svg)

2. Undirected

![](undirected.png)

Graph can be represented as adjacency matrix. If we have way from 1 point to other 
we add `1`, if not `0`.

![](matrix.png)

### Breadth-first search

Find the shortest way from 1 point to the other.

Here we describe graph in this way:
- key === edge
- value === array with connected edges

```javascript
const graph = {}
graph.a = ['b', 'c']
graph.b = ['f']
graph.c = ['d', 'e']
graph.d = ['f']
graph.e = ['f']
graph.f = ['g']

function breadthSearch(graph, start, end) {
    let queue = []
    queue.push(start)
    while (queue.length > 0) {
        const current = queue.shift()
        if (!graph[current]) {
            graph[current] = []
        }
        if (graph[current].includes(end)) {
            return true
        } else {
            queue = [...queue, ...graph[current]]
        }
    }
    return false
}

console.log(breadthSearch(graph, 'a', 'e'))
```

This algorithm always will find the shortest way.

### Dijkstra's algorithm

As opposed to Breadth-first search here we consider the length of vertexes named `weight`.

Workflow:
1. Create a table where we have start point and all other points. Here we store all weights,
that are accessible from the start point and the other as an `infinity`.
![](dijkstra-1.png)
2. Then we add mark already passed edges and add increase weight.
![](dijkstra-2.png)
3. Find shorter way to the point and rewrite the weight
![](dijkstra-3.png)

Here we have objects with weights.

```javascript
const graph = {}
graph.a = {b: 2, c: 1}
graph.b = {f: 7}
graph.c = {d: 5, e: 2}
graph.d = {f: 2}
graph.e = {f: 1}
graph.f = {g: 1}
graph.g = {}

function shortPath(graph, start, end) {
    const costs = {}
    const processed = []
    let neighbors = {}
    Object.keys(graph).forEach(node => {
        if (node !== start) {
            let value = graph[start][node]
            costs[node] = value || Infinity
        }
    })
    let node = findNodeLowestCost(costs, processed)
    while (node) {
        const cost = costs[node]
        neighbors = graph[node]
        Object.keys(neighbors).forEach(neighbor => {
            let newCost = cost + neighbors[neighbor]
            if (newCost < costs[neighbor]) {
                costs[neighbor] = newCost
            }
        })
        processed.push(node)
        node = findNodeLowestCost(costs, processed)
    }
    return costs
}


function findNodeLowestCost(costs, processed) {
    let lowestCost = Infinity
    let lowestNode;
    Object.keys(costs).forEach(node => {
        let cost = costs[node]
        if (cost < lowestCost && !processed.includes(node)) {
            lowestCost = cost
            lowestNode = node
        }
    })
    return lowestNode
}

console.log(shortPath(graph, 'a', 'g'));
```

## Queue 

FIFO - First In First Out. Always add element to the end and remove from the start.