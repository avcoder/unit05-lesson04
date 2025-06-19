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

# Data Structure: Graphs

- A graph is a collection of nodes (vertices) and edges (connections).  It can be:
   - Directed or Undirected
   - Cyclic or Acyclic
   - Weighted or Unweighted
   - More general than trees (no root required, can have cycles).

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
image: /assets/addy.png
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

---
transition: slide-left
---

# Homework

- Work on your "Note-taking" midterm app due June 15 midnight EST
   - can submit before due date if you wish
- Recursion exercises: https://leetcode.com/problem-list/recursion/