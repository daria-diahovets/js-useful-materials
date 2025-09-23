# JavaScript Algorithms

|   № | Content                                                                       |
| --: | ----------------------------------------------------------------------------- |
|   1 | [What is an Algorithm in Programming?](#what-is-an-algorithm-in-programming)  |
|   2 | [Why are Algorithms Important?](#why-are-algorithms-important)                |
|   3 | [Big "O" Notation (Complexity Analysis)](#big-o-notation-complexity-analysis) |
|   4 | [Difficulty Rating of Algorithms](#difficulty-rating-of-algorithms)           |
|   5 | [Linear Search](#linear-search)                                               |
|   6 | [Binary Search (Iterative Approach)](#binary-search-iterative-approach)       |
|   7 | [Selection Sort](#selection-sort)                                             |
|   8 | [Bubble Sort](#bubble-sort)                                                   |
|   9 | [Factorial](#factorial)                                                       |
|  10 | [Fibonachi](#fibonachi)                                                       |
|  11 | [Quick Sort (Hoare's sort)](#quick-sort-hoares-sort)                          |
|  12 | [Binary Search (Recursive Approach)](#binary-search-recursive-approach)       |
|  13 | [Adjacency Matrix](#adjacency-matrix)                                         |
|  14 | [Dijkstra's Algorithm](#dijkstras-algorithm)                                  |

## What is an Algorithm in Programming?

An algorithm is a step-by-step set of instructions to solve a specific problem or perform a computation.
It’s like a recipe in cooking: given some inputs (ingredients), it tells you exactly what steps to follow to reach an output (the dish).

## Why are Algorithms Important?

- They allow programmers to solve problems efficiently.
- The same problem can have multiple solutions, but some are faster, use less memory, or scale better as the input grows.

## Big "O" Notation (Complexity Analysis)

- Big O notation describes how the runtime (or memory usage) of an algorithm grows as the size of input increases.
- It doesn’t measure exact time but gives a mathematical upper bound — how bad things can get as inputs grow large.

**Common complexities:**

- **O(1)** → Constant time (super fast, independent of input size). `Example: accessing an array element by index`.
- **O(log n)** → Logarithmic time. `Example: binary search.`
- **O(n)** → Linear time. `Example: iterating through an array once.`
- **O(n log n)** → Log-linear. `Example: efficient sorting algorithms like merge sort, quicksort.`
- **O(n²)** → Quadratic time. `Example: simple bubble sort, nested loops over arrays.`
- **O(2^n)** → Exponential. `Example: recursive brute force for subsets.`
- **O(n!)** → Factorial. `Example: checking all permutations.`

## Difficulty Rating of Algorithms

In programming (especially in coding interviews or competitions), algorithms are often rated by _difficulty_:

- Easy → Simple loops, arrays, hash maps, strings. Usually O(n) or O(1).
- Medium → Requires some cleverness. Sorting, recursion, binary search, greedy algorithms, O(n log n).
- Hard → Advanced data structures (graphs, trees, dynamic programming), complex problem-solving, sometimes exponential algorithms optimized by pruning.

**For example:**

- Easy: Find the sum of numbers in a list (O(n)).
- Medium: Merge two sorted lists (O(n)).
- Hard: Solve the traveling salesman problem (NP-hard, exponential).

## Linear Search

A simple search algorithm that checks each element of the array one by one until the target item is found or the array ends.

- Time complexity: O(n)

```javascript
const array = [3, 8, 1, 9, 14, 36, 57, 49];
let count = 0;
function linearSearch(array, item) {
  for (let i = 0; i < array.length; i++) {
    count += 1;
    if (array[i] === item) {
      return i;
    }
  }
  return null;
}
console.log("The index of element: ", linearSearch(array, 49)); // 7
console.log("Count of iteration: ", count); // 8
```

## Binary Search (Iterative Approach)

An efficient search algorithm that works on sorted arrays by repeatedly dividing the search range in half until the target is found or the range is empty.

- Time complexity: O(log n)

```javascript
const array = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15];
let count = 0;
function binarySearch(array, target) {
  let start = 0;
  let end = array.length - 1;
  let middle;
  let found = false;
  let position = -1;
  while (found === false && start <= end) {
    count += 1;
    middle = Math.floor((start + end) / 2);
    if (arr[middle] === target) {
      found = true;
      position = middle;
      return position;
    } else if (arr[middle] < target) {
      start = middle + 1;
    } else {
      end = middle - 1;
    }
  }
  return position;
}

console.log("The index of element:", binarySearch(array, 14));
console.log("The count of iteration:", count);
```

## Selection Sort

Selection Sort

A sorting algorithm that repeatedly finds the minimum element from the unsorted portion of the array and swaps it with the first unsorted element.

- Time complexity: O(n²)

```javascript
const array = [0, 3, 8, 1, 9, 14, 36, 57, 23, -1, -5, 25, 1, 9, 3];
let count = 0;
function selectionSort(array) {
  for (let i = 0; i < array.length; i++) {
    let indexMin = i;
    for (let j = i + 1; j < array.length; j++) {
      if (array[j] < array[indexMin]) {
        indexMin = j;
      }
      count += 1;
    }
    let temp = array[i];
    array[i] = array[indexMin];
    array[indexMin] = temp;
  }
  return array;
}
console.log("selectionSort output:", selectionSort(array));
console.log("The count of iteration:", count);
```

## Bubble Sort

A simple sorting algorithm that repeatedly compares and swaps adjacent elements if they are in the wrong order, making larger elements "bubble up" to the end.

- Time complexity: O(n²)

```javascript
const array = [0, 3, 8, 1, 9, 14, 36, 57, 23, -1, -5, 25, 1, 9, 3];
let count = 0;

function bubbleSort(array) {
  for (let i = 0; i < array.length; i++) {
    for (let j = 0; j < array.length; j++) {
      if (array[j] > array[j + 1]) {
        let temp = array[j];
        array[j] = array[j + 1];
        array[j + 1] = temp;
      }
      count += 1;
    }
  }
}

bubbleSort(array);
console.log("bubbleSort: ", array);
console.log("The count of iteration:", count);
```

## Factorial

A recursive algorithm that multiplies a number n by all positive integers less than it, down to 1.

- Time complexity: O(n)

```javascript
const factorial = (n) => {
  if (n === 0) {
    return 1;
  }
  return n * factorial(n - 1);
};
console.log(factorial(5));
```

## Fibonachi

A recursive algorithm that generates the n-th Fibonacci number, where each number is the sum of the two preceding ones (`F(n) = F(n-1) + F(n-2)`), with base cases `F(1) = 1`, `F(2) = 1`.

- Sequence: 1, 1, 2, 3, 5, 8, 13, …
- Time complexity: O(2ⁿ) (very inefficient due to repeated recalculations).

```javascript
const fibonachi = (n) => {
  if (n === 1 || n === 2) {
    return 1;
  }
  return fibonachi(n - 1) + fibonachi(n - 2);
};
console.log(fibonachi(6)); // 8
```

## Quick Sort (Hoare's sort)

The algorithm operates on the so-called **"divide and conquer"** principle. The idea is that we divide the array into subarrays, each time recursively. We select a pivot element for each array (it can be chosen randomly, but the central element is most often chosen). We iterate through the array, adding all elements with a value smaller than the pivot to one array, and all elements with a value greater than the pivot to the other. After this operation, we have two arrays with values ​​smaller than the pivot and greater than the pivot. The same operation is performed for each of these arrays, and this process continues until the array length equals one. At the end, all this is glued together into one array.

```javascript
const array = [0, -1, -5, 10, 35, 59, -14, 4, 15, -9, 21, 95];
let count = 0;

function quickSort(array) {
  if (array.length <= 1) {
    return array;
  }
  let pivotIndex = Math.floor(array.length / 2);
  let pivot = array[pivotIndex];
  let less = [];
  let greater = [];
  for (let i = 0; i < array.length; i++) {
    count += 1;
    if (i === pivotIndex) {
      continue;
    }
    if (array[i] < pivot) {
      less.push(array[i]);
    } else {
      greater.push(array[i]);
    }
  }
  return [...quickSort(less), pivot, ...quickSort(greater)];
}
console.log(quickSort(array));
console.log(count);
```

## Binary Search (Recursive Approach)

A divide-and-conquer search algorithm that works on sorted arrays. It repeatedly compares the target with the middle element, then recursively searches the left or right half until the target is found or the range is empty.

- Time complexity: O(log n)
- Space complexity: O(log n) _(because of recursive function calls on the call stack)_.

```javascript
const array = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15];
let count = 0;
function recursiveBinarySearch(array, item, start, end) {
  let middle = Math.floor((start + end) / 2);
  count += 1;
  if (item === array[middle]) {
    return middle;
  }
  if (item < array[middle]) {
    return recursiveBinarySearch(array, item, start, middle - 1);
  } else {
    return recursiveBinarySearch(array, item, middle + 1, end);
  }
}
console.log(recursiveBinarySearch(array, 10, 0, array.length));
console.log(count);
```

## Graphs, Breadth-first search in graph

- A graph is an abstract data structure representing a set of vertices and a set of edges (an example of a graph is a map).

![Breadth-first search in graph.](/images/github-graph.png)

- This algorithm will use a queue data structure.
- A queue (FIFO - First In First Out) - is a data structure consisting of certain elements. The principle is that elements are added to the end of the structure and retrieved from the beginning (a real-life example: a checkout line).

![Queue structure.](/images/github-queue.png)

```javascript
const graph = {};
graph.a = ["b", "c"];
graph.b = ["f"];
graph.c = ["d", "e"];
graph.d = ["f"];
graph.e = ["f"];
graph.f = ["g"];

function breadthSearch(graph, start, end) {
  let queue = [];
  queue.push(start);
  while (queue.length > 0) {
    const current = queue.shift();
    if (!graph[current]) {
      graph[current] = [];
    }
    if (graph[current].includes(end)) {
      return true;
    } else {
      queue = [...queue, ...graph[current]];
    }
  }
  return false;
}
console.log(breadthSearch(graph, "a", "g")); // true
```

## Adjacency Matrix

An adjacency matrix is a square grid that represents the connections (edges) between nodes (vertices) in a graph. It's an n x n matrix for a graph with n vertices, where the value at position (i, j) is 1 if there's an edge from vertex i to vertex j, and 0 otherwise. For undirected graphs, the matrix is symmetric; for directed graphs, it's not necessarily symmetric.

![Adjacency Matrix example.](/images/github-matrix.png)

```javascript
const matrix = [
  [0, 1, 1, 0, 0, 0, 0],
  [0, 0, 0, 0, 1, 0, 0],
  [0, 0, 0, 1, 0, 1, 0],
  [0, 0, 0, 0, 1, 0, 0],
  [0, 0, 0, 0, 0, 0, 1],
  [0, 0, 0, 0, 1, 0, 0],
  [0, 0, 0, 0, 0, 0, 0],
];
```

## Dijkstra's Algorithm

Dijkstra's algorithm finds the shortest path from a single starting vertex to all other vertices in a weighted graph, provided all edge weights are non-negative. The algorithm works by iteratively selecting the unvisited vertex with the smallest known distance from the source, marking it as visited, and updating the distances to its adjacent vertices. It's a greedy algorithm that ensures the shortest path is found for each node by progressively exploring the graph.

![Dijkstra's Algorithm.](/images/github_dijkstra.png)

```javascript
const graph = {};
graph.a = { b: 2, c: 1 };
graph.b = { f: 7 };
graph.c = { d: 5, e: 2 };
graph.d = { f: 2 };
graph.e = { f: 1 };
graph.f = { g: 1 };
graph.g = {};

function shortPath(graph, start, end) {
  const costs = {};
  const processed = [];
  let neighbors = {};
  Object.keys(graph).forEach((node) => {
    if (node !== start) {
      let value = graph[start][node];
      costs[node] = value || 100000000; // Infinity
    }
  });
  let node = findNodeLowestCost(costs, processed);
  while (node) {
    const cost = costs[node];
    neighbors = graph[node];
    Object.keys(neighbors).forEach((neighbor) => {
      let newCost = cost + neighbors[neighbor];
      if (newCost < costs[neighbor]) {
        costs[neighbor] = newCost;
      }
    });
    processed.push(node);
    if (node === end) break;
    node = findNodeLowestCost(costs, processed);
  }
  return costs;
}

function findNodeLowestCost(costs, processed) {
  let lowestCost = 100000000;
  let lowestNode;
  Object.keys(costs).forEach((node) => {
    let cost = costs[node];
    if (cost < lowestCost && !processed.includes(node)) {
      lowestCost = cost;
      lowestNode = node;
    }
  });
  return lowestNode;
}

console.log(shortPath(graph, "a", "g"));
```
