---
# You can also start simply with 'default'
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: /assets/intro.jpg
# some information about your slides (markdown enabled)
title: Software Development | Foundations
info: |
  ## Software Development | Foundations
# apply unocss classes to the current slide
class: text-left
drawings:
  persist: false
transition: slide-left
mdc: true
---

# Algorithms and Data Structures
Algorithms and Structural Foundations - part 4/8

- [ ] Trees
- [ ] Graphs
- [ ] Dijkstra's Algorithm

<div class="abs-br m-6 text-xl">
  <a href="https://github.com/slidevjs/slidev" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

---
transition: slide-left
---

# Recap
Imagine we have a sorted array: `[1, 2, 3, 4, 5, 6, 7]`

- We can create stacks/queues using:
   - linked list data structure
- Binary Search allowed us to use recursion to search left side vs right side
   - to do so required us to take the array length and divide by 2 then round it to get midpoint 
   - Can we do binary search on a linked list? 
      - Do we have a way to "go left" using a single linked list?
      - Do we have a way to pick the middle?
- Problem: Need a better data structure that's better than O(n) to search/insert/delete a sorted list 

---
transition: slide-left
---

# Big O Recap

<img src="/assets/bigo.jpg" width="800">

---
transition: slide-left
---

# Data Structure: Trees

- A tree is a non-linear hierarchical data structure. (2-dimensional)
- Unlike arrays or linked lists, trees branch out.
- Consists of nodes connected by edges.
- Has one root node and zero or more child nodes.
- Common types: Binary Tree, Binary Search Tree, AVL Tree.

<img src="/assets/tree.webp" width="700">

<!--
-->

---
transition: slide-left
---

# Why Use Trees?

- Efficient searching and sorting (ex: Binary Search Trees).  
- Used in parsing expressions, DOM structure in browsers.
- Manage hierarchical data (e.g., file systems, organization charts).
- Support for auto-complete, AI game trees, and databases.

<img src="/assets/bst.png" width="700">

---
transition: slide-left
---

# Tree Terminology

| **Term**    | **Definition**                                                          |
| ----------- | ----------------------------------------------------------------------- |
| **Node**    | A single element in a tree that holds a value and may have child nodes. |
| **Root**    | The topmost node of the tree; has no parent.                            |
| **Child**   | A node that descends from another node (its parent).                    |
| **Parent**  | A node that has one or more children.                                   |
| **Leaf**    | A node that has no children.                                            |
| **Edge**    | A connection between two nodes (parent to child).                       |
| **Depth**   | The number of edges from the root node to a given node.                 |

---
transition: slide-left
---

# Binary Search Pseudocode using Trees

```md
Function search(value):
    Set current = root

    While current is not null:
        If value is equal to current.value:
            Return true (value found)

        If value is less than current.value:
            Move current to current.left

        Else:
            Move current to current.right

    Return false (value not found)
```

- Instead of doing basic math like dividing array by 2 then rounding in order to get the midpoint, we just follow the pointers which gives us O(log n)
- Tradeoff: 
   - more space is used
   - What happens if it just happens that the numbers inputted are always put on the right hand side?

---
transition: slide-left
---

# Big O for Trees

| **Operation**           | **Balanced BST** (e.g., [AVL](https://en.wikipedia.org/wiki/AVL_tree), [Red-Black](https://en.wikipedia.org/wiki/Red%E2%80%93black_tree)) | **Unbalanced BST** |
| ----------------------- | --------------------------------------- | ------------------ |
| **Search**              | O(log n)                                | O(n)               |
| **Insert**              | O(log n)                                | O(n)               |
| **Delete**              | O(log n)                                | O(n)               |
| **Traversal (DFS/BFS)** | O(n)                                    | O(n)               |
| **Access Min/Max**      | O(log n)                                | O(n)               |


---
transition: slide-left
---

# Tree Creation: Usage

```js
const root = new TreeNode(1);
const child1 = new TreeNode(2);
const child2 = new TreeNode(3);
root.addChild(child1);
root.addChild(child2);
```

       1
     /   \
    2     3

```js
// basic objects analogy:
const son = { name: 'Bob' }
const daughter = { name: 'Christie' }

const mother = {
  name: 'Ashley',
  children: [son, daughter]
}
```

---
transition: slide-left
---

# Tree Operations

| **Operation**             | **Description**                                                                 |
| ------------------------- | ------------------------------------------------------------------------------- |
| **Insert**                | Adds a new node to the tree, maintaining binary search tree (BST) structure     |
| **Search**                | Finds a node with a specific value                                              |
| **Delete**                | Removes a node and restructures the tree if needed                              |
| **In-order Traversal**    | Visits nodes in left-root-right order (outputs sorted values in a BST)          |
| **Find Min**              | Locates the node with the smallest value (leftmost node in a BST)               |
| **Find Max**              | Locates the node with the largest value (rightmost node in a BST)               |
| **Height**                | Measures the longest path from the root to a leaf node                          |
| **Check Balanced**        | Determines if the tree is height-balanced (difference in subtree heights ≤ 1)   |



---
transition: slide-left
---

# Tree Implementation

```md
1. Define a Node with:
   - A value
   - A list to store child nodes

2. Create a function to add a child to a node:
   - Add the child to the node's list of children
```

```js
class TreeNode {
  constructor(value) {
    this.value = value;
    this.children = [];
  }

  addChild(node) {
    this.children.push(node);
  }
}
```

---
transition: slide-left
---

# Story about Euler

<img src="/assets/Euler2.jpg">

https://www.encyclopedia.com/science/encyclopedias-almanacs-transcripts-and-maps/birth-graph-theory-leonhard-euler-and-konigsberg-bridge-problem

---
transition: slide-left
---

# Data Structure: Graphs

- A graph is a collection of nodes (vertices) and edges (connections).  It can be:
   - Directed or Undirected
   - Cyclic or Acyclic
   - Weighted or Unweighted
   - More general than trees (no root required, can have cycles).
   - Q: Imagine how you might code this?

<img src="/assets/graph.webp" width="700">

---
transition: slide-left
---

# Why use Graphs?

- Social networks (friends, followers).
- Routing algorithms (Google Maps).
- Recommendation engines (Amazon, Netflix).
- Dependency graphs in compilers and build systems.
- Knowledge graphs for AI and search engines.

<img src="/assets/facebook.jpeg" width="700">


---
transition: slide-left
---

# Graph Terminology

| **Term**               | **Definition**                                                                 |
| ---------------------- | ------------------------------------------------------------------------------ |
| **Vertex (Node)**      | A fundamental unit of a graph representing a point or object                   |
| **Edge**               | A connection between two vertices                                              |
| **Adjacency**          | Two vertices are adjacent if they are connected directly by an edge            |
| **Adjacent List**      | A way to represent a graph where each vertex stores a list of its neighbors    |
| **Directed Graph**     | A graph where edges have a direction (u → v)                                   |
| **Undirected Graph**   | A graph where edges have no direction (u — v)                                  |
| **Weighted Graph**     | A graph where edges have numerical values (weights) associated with them       |
| **Cycle**              | A path where the first and last vertex are the same, and no other nodes repeat |

---
transition: slide-left
---

# 2 Ways to Represent a Graph

- Adjacency List (most used) vs Adjacency List (takes up too much memory space O(V^2))

<img src="/assets/adjvs.svg" width="900">

---
transition: slide-left
---

# Big O for Graph

| **Operation / Algorithm**           | **Adjacency List** | **Adjacency Matrix**  | **Notes**                                           |
| ----------------------------------- | ------------------ | --------------------- | --------------------------------------------------- |
| **Add Vertex**                      | O(1)               | O(n²) (resize needed) | List is more efficient for dynamic growth           |
| **Add Edge**                        | O(1)               | O(1)                  | Constant time in both                               |
| **Remove Vertex**                   | O(V + E)           | O(n²)                 | Must remove associated edges                        |
| **Remove Edge**                     | O(V) (search list) | O(1)                  | Matrix allows direct access                         |
| **Check Edge Exists**               | O(V)               | O(1)                  | Matrix is faster for dense graphs                   |
| **DFS / BFS Traversal**             | O(V + E)           | O(V²)                 | Depends on the number of vertices (V) and edges (E) |
| **Dijkstra’s Algorithm (Min Heap)** | O((V + E) log V)   | O(V²)                 | Efficient with priority queue and list              |



---
transition: slide-left
---

# Graph Operations

| **Operation**                  | **Description**                                                                     |
| ------------------------------ | ----------------------------------------------------------------------------------- |
| **Add Vertex**                 | Adds a new node (vertex) to the graph                                               |
| **Add Edge**                   | Creates a connection (edge) between two vertices                                    |
| **Remove Vertex**              | Deletes a vertex and all edges connected to it                                      |
| **Remove Edge**                | Deletes the connection between two vertices                                         |
| **Check Edge Exists**          | Determines whether there is a connection between two vertices                       |
| **Get Neighbors**              | Returns a list of vertices directly connected to a given vertex                     |
| **DFS (Depth-First Search)**   | Traverses the graph by exploring as far as possible along each branch               |
| **BFS (Breadth-First Search)** | Traverses the graph level by level, exploring neighbors first                       |



---
transition: slide-left
---

# Graph Usage 

```js
// Create a graph
const graph = new Graph();
graph.addVertex(1);
graph.addVertex(2);
graph.addEdge(1, 2);
```

1 —— 2

---
transition: slide-left
---

# Graph Usage (pg.2)

```js
// Create the graph
const fbGraph = new FacebookGraph();

// Add users
['Alice', 'Bob', 'Carla', 'David', 'Emma'].forEach(user => fbGraph.addUser(user));

// Add friendships
fbGraph.addFriendship('Alice', 'Bob');
fbGraph.addFriendship('Alice', 'Carla');
fbGraph.addFriendship('Bob', 'David');
fbGraph.addFriendship('Carla', 'David');
fbGraph.addFriendship('David', 'Emma');
```

       Alice
       /   \
    Bob    Carla
      \   /
      David
        |
       Emma



---
transition: slide-left
---

# Graph Implementation 

1. Define a Graph with:
   - A map or dictionary to store each vertex and its list of connected vertices (adjacency list)
2. Create a function to add a vertex:
   - If the vertex does not exist in the adjacency list, add it with an empty list
3. Create a function to add an edge between two vertices:
   - Add each vertex to the other’s list (for an undirected graph)

```js
class Graph {
  constructor() { this.adjacencyList = new Map() }

  addVertex(vertex) {
    if (!this.adjacencyList.has(vertex)) {
      this.adjacencyList.set(vertex, []);
    }
  }

  addEdge(v1, v2) {
    this.adjacencyList.get(v1).push(v2);
    this.adjacencyList.get(v2).push(v1); // undirected
  }
}
```

---
transition: slide-left
---

# Trees vs Graphs

| Feature   | Tree            | Graph                  |
| --------- | --------------- | ---------------------- |
| Structure | Hierarchical    | Network (flexible)     |
| Root Node | Exactly one     | Not required           |
| Cycles    | No              | Can have cycles        |
| Direction | Always directed | Directed or undirected |


---
layout: image-right
transition: slide-left
image: /assets/fcc.png
backgroundSize: 400px 300px
class: text-left
---

# 10 minute break

🍦 Cool Tips, Trends and Resources:
- 🌴 [DOM Tree](https://cdn.sanity.io/images/gpji8x82/production/5910b5ee6fa6049fedc86092a3bc6547d64d15b5-960x540.jpg?w=800)
- 🗃️ [File System Tree](https://campmetrics.com/wp-content/uploads/elementor/thumbs/file-tree-qm5wri7mlgkq188exraancw854iiboxkaoathsos8g.png)
- 🗺️ [Map Graph](https://miro.medium.com/v2/resize:fit:1400/1*JWLgsI1hRULw6xTS1AGP8A.png)
- 👀 [Visual Go](https://visualgo.net/en)
- 😵‍💫 [Data Structure Visualization](https://www.cs.usfca.edu/~galles/visualization/Algorithms.html)

<br>
<hr>
<br>

- 🧪 [Enter anonymous lab questions](https://docs.google.com/forms/d/e/1FAIpQLSevvGARdHQikso-uLqFCO481MABKE5HofuSrlzEPMNQ2ZLykw/viewform?usp=dialog)
- ℹ️ [Course feedback survey](https://circuitstream.typeform.com/to/ZoyYk7px#course_id=SoftwareAN&instructor=9514)

---
transition: slide-left
---

# Dijkstra's Algorithm

- Dijkstra’s Algorithm finds the shortest path from a starting node to all other nodes in a weighted graph
- It works with:
   - Positive edge weights only
   - Directed or undirected graphs
- Used in: GPS navigation, Network routing, Pathfinding in games

<img src="/assets/dij2.jpg" width="500">

---
transition: slide-left
---

# Key Concepts

| Term               | Definition                                     |
| ------------------ | ---------------------------------------------- |
| **Vertex**         | A node in the graph                            |
| **Edge**           | A connection between two vertices              |
| **Weight**         | Cost to travel from one node to another        |
| **Distance Table** | Stores shortest known distances from the start |
| **Visited Set**    | Tracks nodes whose shortest path is finalized  |
| **Priority Queue** | Picks the next closest node to explore         |



---
transition: slide-left
---

# Pseudocode of Dijkstra's Algorithm (v.1)

1. Imagine you are starting in your hometown.
2. Write down how far each city is from your hometown:
    - Your hometown is 0 steps away.
    - Every other city is “really far” (we can call it infinity).
3. Make a list of all cities you need to visit.
4. While you still have cities to visit:
    - a. Look at the city on your list that is the closest so far.
    - b. From that city, look at every city it connects to (its neighbors).
    - c. For each neighbor:
        - Add the number of steps from your hometown to the city you’re on,
          plus the number of steps to get to the neighbor.
        - If this total is smaller than what you wrote before for that neighbor,
          change the number to the smaller one.
    d. You are now done with the current city. Cross it off your list.
5. When you’ve visited all the cities, you’ll know the shortest way to every city!

---
transition: slide-left
---

# Pseudocode of Dijkstra's Algorithm (v.2)

1. Start by assigning a distance value to every node:
    - Set the distance to the starting node as 0.
    - Set the distance to all other nodes as infinity (∞) because we haven't found a path to them yet.
2. Create a list (or priority queue) of all the nodes that need to be checked.
3. While there are still nodes to check:
    a. Pick the node with the smallest distance value (let's call this the "current node").
    b. Look at all the neighboring nodes connected to the current node.
    c. For each neighbor:
        - Calculate the distance from the start node to this neighbor by going through the current node.
        - If this new path is shorter than the distance we had recorded before:
            - Update the shortest distance for that neighbor.
    d. Once done checking all neighbors, mark the current node as "visited" so we don't check it again.
4. When all nodes have been visited, the shortest distance to each node from the start is known.



---
transition: slide-left
---

# Pseudocode of Dijstra's Algorithm (v.3) 

```md
function dijkstra(graph, startNode):
    Create a map called distances, where every node is set to Infinity    // Step 1: Set up distances and visited
    Set distances[startNode] to 0

    Create a priority queue (min-heap) and add startNode with distance 0

    Create a set to keep track of visited nodes

    while priority queue is not empty: // Step 2: Loop until we’ve checked all nodes
        currentNode ← remove the node with the lowest distance from the queue // Get the node with smallest distance

        if currentNode has already been visited:
            skip to the next iteration

        mark currentNode as visited

        for each neighbor of currentNode in graph:         // Step 3: Check all neighboring nodes
            edgeWeight ← distance from currentNode to neighbor
            newDistance ← distances[currentNode] + edgeWeight

            if newDistance < distances[neighbor]:
                update distances[neighbor] to newDistance
                add neighbor to priority queue with newDistance

    return distances
```

---
transition: slide-left
---

# Exercise: 
Find the shortest path from 0 to 4

<img src="/assets/dij3.png" width="550">

---
transition: slide-left
---


# Homework

- Start thinking about which of the 4 topics you'll use for your "Algorithm and Structural Foundation" assignment due July 20
   - 4 Topics will be listed here: https://unit05-lesson5to8.netlify.app/
- Tree exercises: https://leetcode.com/problem-list/tree/
- Graph exercises: https://leetcode.com/problem-list/graph/