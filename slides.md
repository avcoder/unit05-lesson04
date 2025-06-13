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

<!--
-->

---
transition: slide-left
layout: center
class: text-center
---

# In ASCII, the capital `A` has value 65.  Yet in C, I can set an int variable to 65
How does the computer know how to interpret `01000001`?

---
transition: slide-left
---

# Recap (pg.1)

```c
char ch = 65;     // or 'A'
int num = 65;
```

- At the binary level, both ch and num may store the same value (01000001), but:
   - char ch is interpreted as a character → 'A'
   - int num is interpreted as a number → 65
- They're both just bytes in memory. The difference lies in how the C compiler and standard library interpret or print them.

| Declared As | Meaning         | Output with `printf`      |
| ----------- | --------------- | ------------------------- |
| `char ch`   | ASCII character | `printf("%c", ch);` → A   |
| `int num`   | Integer value   | `printf("%d", num);` → 65 |
| `char ch`   | Integer value   | `printf("%d", ch);` → 65  |


---
transition: slide-left
---

# Recap (pg.2)
- Q: How is an array arranged in memory?

<img src="/assets/memory.jpg" width="500px">

---
transition: slide-left
---

# Recap (pg.3)

- Q: What is [Big O notation](https://www.bigocheatsheet.com/)?
- Q: What's the Big O notation for accessing an element in the array?
- Q: What's the Big O notation for inserting a new element?
- Q: What's the Big O notation for deleting a new element?
- Q: Are arrays growable?
- Q: In C, what are the 2 possible values we can output for any variable in memory?
   - in JS, how can we access the value of a variable?
   - in JS, how can we access the address of a variable?
- Q: What was the catch in C when declaring an array?
   - Potential issue: What if we wanted to insert an element in the array?
   - Q: List alternative solutions to this issue?


<!--
- char str[] = "Hello";
- char str[] = { 'H', 'e', 'l', 'l', 'o', '\0' };
- Big O = if space not available O(n)
- 2 possible values = address of memory cell, value written in memory cell
- in JS you cannot access the memory address of a variable directly.
- catch = size must be known at compile time.  Can't resize. 
- issue = takes time array to bigger array; can't accidentally overwrite 'h' for 'hello'
-->

---
transition: slide-left 
layout: center
class: text-center
---

# What if we could structure our data, such that we can connect random allocated memory blocks  instead of contiguous memory blocks?
Like: connect-the-dots

---
transition: slide-left
---

# Data Structure: Linked Lists 
Can we solve the problem of copying an entire array to a new location in memory when inserting?

<img src="/assets/llist.png">

- Each node contains: 
   - a value (data, whose value can be anything. ex: int)
   - a reference (pointer) to the next node (whose value is the address of the next node in memory)
- Q: Does inserting a new element in our list solve the problem we originally had with contiguous memory
- Q: What is the Big O notation for inserting/deleting a new element at the beginning of a linked list?
- Q: What is the Big O notation for inserting/deleting a new element at the end of a linked list?
   - How might we do better for inserting/deleting at end?
- Q: What is the Big O notation for accessing an element in a linked list?

<!--
- O(1) for inserting a new element at beginning of a linked list
- O(n) for inserting a new element at end of a linked list
- Unless you have tail node then it's O(1) for inserting at end
- O(n) for accessing an element in a linked list since you must traverse
-->

---
transition: slide-left
---

# Exercise: Arrays vs Linked Lists

| Feature                       | **Array**                                         | **Linked List**                                   |
| ----------------------------- | ------------------------------------------------- | ------------------------------------------------- |
| **Memory Layout**             | Contiguous memory                                 | Non-contiguous memory                             |
| **Access Time**               | `O(?)` random access via index              | `O(?)` traversal needed                     |
| **Insertion/Deletion (middle)**        | `O(?)` elements need shifting             | `O(?)`                    |
| **Memory Per element Overhead**           | Low (just data)                                   | High (extra pointer per node)                     |
| **Implementation Simplicity** | Simpler                                           | More complex (especially for doubly linked lists) |
| **Use Case Suitability**      | Best for random access and known-size collections | Best for frequent insertions/deletions            |

<!-- 
- Access Time: O(1) vs O(n)
- Insertion/Deletion (middle): O(n) vs O(1)

-->

---
class: text-center
layout: center
transition: slide-left
---

# Which DS could be implemented using Linked Lists?

<img src="/assets/ds1.gif" width="400px" style="display: inline-block">

---
transition: slide-left
---

# Static Memory Allocation in C - Arrays

```c
#include <stdio.h>

int main(void) {
    int list[3];

    list[0] = 1;
    list[1] = 2;
    list[2] = 3;

    for (int i = 0; i < 3; i++) {
        printf("%d at %p\n", list[i], (void*)&list[i]);
    }
}
```

---
transition: slide-left
---

# Dynamic Memory Allocation in C - Arrays

```c
#include <stdio.h>
#include <stdlib.h>

int main(void) {
    int list[3] = {1, 2, 3}; // static memory allocation
    int *list2 = malloc(4 * sizeof(int)); // allocate memory for 4 integers

    if (list2 == NULL) { 
      return 1; // Memory allocation failed
    } 

    for (int i = 0; i < 3; i++) {
      list2[i] = list[i]; // copy values from static array to dynamic array
    }
    list2[3] = 4; // add a new element

    for (int i = 0; i < 4; i++) {
        printf("%d at %p\n", list2[i], (void*)&list2[i]);
    }

    free(list2); // free the dynamically allocated memory
}
```

---
transition: slide-left
---

# Equivalent in JS
JS doesn't have memory allocation like malloc/free.  Rather arrays are dynamic and managed automatically

```js
function main() {
    const list = [1, 2, 3];  // Static array equivalent
    const list2 = new Array(4); // Dynamic array with extra space - just create a new array

    // Copy first 3 elements from list to list2
    for (let i = 0; i < 3; i++) {
        list2[i] = list[i];
    }

    // Add new element
    list2[3] = 4;

    // Print values with their indices (JS has no direct access to memory addresses)
    for (let i = 0; i < 4; i++) {
        console.log(`Value: ${list2[i]}, Index: ${i}`);
    }
    // No need to free memory in JS, garbage collector handles it
}

main();
```

---
transition: slide-left
---

# btw, Insight Aha moment in JS

```js
2 === 2 // true
'a' === 'a' // true
true === true // true

// Why are the below false?
[] === [] // false
{} === {} // false

const a = [];
const b = [];
console.log(a === b); // false

const obj1 = {};
const obj2 = {};
console.log(obj1 === obj2); // false

const c = []
c.push(1); allowed
c = [2] // Error: Assignment to constant variable

const d = {};
d.name = 'John'; // allowed
d = { name: 'John' }; // Error: Assignment to constant variable
```

---
transition: slide-left
---

# Linked Lists in JS (pg.1)

```
// pseudo-code
CLASS Node
    PROPERTY value
    PROPERTY next

    FUNCTION constructor(val)
        SET value TO val
        SET next TO null
    END FUNCTION
END CLASS
```
```js
// in JS
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}
```

---
transition: slide-left
---

# Linked Lists in JS (pg.2)

```js
class LinkedList {
  constructor() {
    this.head = null; // Pointer to the first node; SET it to NULL initially
    this.size = 0; // Number of nodes in the list; SET it to 0 initially
  }

  // Insert new node at the end
  append(value) {
    const newNode = new Node(value);

    if (!this.head) { // IF head IS null, it means the list is empty
      this.head = newNode; // Set head to the new node
    } else {
      let current = this.head; // Start from the head
      while (current.next) { // Traverse to the last node
        current = current.next; 
      }
      current.next = newNode; // Set the next of the last node to the new node
    }

    this.size++; // Increment the size of the list
  }
```

---
transition: slide-left
---

# Linked Lists in JS (pg.3)

```js
  // Print list values
  print() {
    let current = this.head;
    let result = '';

    while (current) {
      result += current.value + ' -> ';
      current = current.next;
    }
    result += 'null';
    console.log(result);
  }

  // Search for a value (returns true/false)
  contains(value) {
    let current = this.head;

    while (current) {
      if (current.value === value) return true;
      current = current.next;
    }

    return false;
  }
}
```

---
transition: slide-left
---

# Linked Lists in JS (pg.4)
Usage 

```js
const list = new LinkedList();

list.append(10);
list.append(20);
list.append(30);

list.print();             // Output: 10 -> 20 -> 30 -> null
console.log(list.contains(20));  // Output: true
console.log(list.contains(40));  // Output: false

```

---
transition: slide-left
---

# Summary

- Arrays can give us contiguous memory allocation, but they have limitations when it comes to resizing and inserting/deleting elements.
- Linked Lists allow us to dynamically allocate memory and connect nodes, making it easier to insert and delete elements without needing to copy the entire structure, but they have slower access times and more memory overhead.
- Can we get the best of both worlds?
- So far, we've been dealing with one-dimensional data structures.
- What if we need to store more complex data, like a collection of items with unique identifiers, or a mapping of keys to values?
- What if we need to access elements by a unique key rather than an index?



---
transition: slide-left
---

# Dictionaries

- What is a dictionary?
   - A data structure that stores key-value pairs (like a JS object)
   - Keys are unique identifiers for values
   - Values hold associated ata
   - Similar to a real-world dictionary where you look up a word (key) to find its definition (value)
- example in JS:
```js
const dictionary = {
  'apple': 'A fruit that is red or green',
  'banana': 'A long yellow fruit',
  'carrot': 'An orange vegetable'
};
console.log(dictionary['apple']); // Output: A fruit that is red or green
console.log(dictionary.banana); // Output: A long yellow fruit
```

- Operations on Dictionaries include: Insert, Search, Delete, Update
- Average O(1) for insert, search, and delete operations
- Worst-case O(n) if many collisions occur (e.g., all keys hash to the same index)

---
transition: slide-left  
---

# How is a Dictionary Formed in Memory?

- Internally uses hash tables or arrays (think hashing function like `bcrypt` from cybersecurity class)
- Keys are converted to hash codes (unique numerical representations OR index)
- Values are stored at the index corresponding to the hash code
- Handles collisions (when two keys hash to the same index) using techniques like chaining or open addressing

<img src="/assets/dict.png" width="300px" style="background-color: #fff; display: block; margin: 0 auto">

---
transition: slide-left
layout: center
class: text-center
---

# Does that mean each JS object's key is actually hashed into some alphanumeric code?
Yes

---
transition: slide-left
---

# JS objects are hashed

- When you declare an object like:
```js
const obj = {
  name: "Alice",
  age: 25,
};
```

- Internally: ✅ Yes, string keys are hashed into numeric values (not visible to you).
- Externally: ❌ You still see your keys as-is, e.g., "name" or "age" — not the hash codes.
- Maps those hashes to memory locations (or internal table buckets)
- Stores the associated values (like "Alice", 25, etc.) at hash-computed locations


The hash codes are used purely for efficient lookup behind the scenes.

---
transition: slide-left
---

# Hashing   
Hashing is the process of converting an input (or 'key') into a fixed-size string of bytes.

<img src="/assets/hash.png" style="display: block; margin: 0 auto" />

- Analogy: placing 52 playing cards by their suit -- into 4 boxes.

---
transition: slide-left
---

# Hash Tables
A combination of an array and a linked list

- Each index in the array is a bucket that can hold multiple key-value pairs (in case of collisions)
- Each bucket can be implemented as a linked list or another data structure to handle collisions

<img src="/assets/hashtable.svg" style="background-color: #fff; display: block; margin: 0 auto" />

- Potential issue = Collisions: when two keys hash to the same index

---
transition: slide-left
---

# Hash Table / Dictionaries - Big O
Technically a dictionary has worst case of O(n), but in practice, it is often O(1) due to good hash functions and collision resolution strategies.

| Operation  | Average Case | Worst Case |
| ---------- | ------------ | ---------- |
| **Insert** | O(1)         | O(n)       |
| **Search** | O(1)         | O(n)       |
| **Delete** | O(1)         | O(n)       |

- What causes the worst case?
   - Poor hash function leading to many collisions
   - All keys hashing to the same index
   - Inefficient collision resolution strategy

---
transition: slide-left  
---

# Pseudo-code for a Dictionary

```
class DictionaryEntry {
    key
    value
}

class Dictionary {
    entries = array of DictionaryEntry
    add(key, value)
    get(key)
    remove(key)
}
```

---
transition: slide-left  
---

# Hash Table / Dictionaries in JS (pg.1)
Usage:

```js
const dict = new HashTable();

dict.set("name", "Alice");
dict.set("age", 30);
dict.set("job", "Engineer");

console.log(dict.get("name"));  // Alice
console.log(dict.get("age"));   // 30

dict.set("age", 31);            // Update value
console.log(dict.get("age"));   // 31

dict.remove("job");
console.log(dict.get("job"));   // undefined

dict.print();                   // See bucket contents
```

---
transition: slide-left  
---

# Hash Table / Dictionaries in JS (pg.2)

```js
class Dictionary {
  constructor() {
    this.entries = {}; // Using an object to store key-value pairs
  }

  add(key, value) {
    this.entries[key] = value; // Add or update the key-value pair
  }

  get(key) {
    return this.entries[key]; // Retrieve the value for the given key
  }

  remove(key) {
    delete this.entries[key]; // Remove the key-value pair
  }
}
```

---
transition: slide-left
---

# Hash Table / Dictionaries in JS (pg.3)

```js
class HashTable {
  constructor(size = 10) {
    this.buckets = new Array(size).fill(null).map(() => []);
    this.size = size;
  }

  // Simple hash function
  hash(key) {
    let hash = 0;
    for (let char of key) {
      hash += char.charCodeAt(0);
    }
    return hash % this.size;
  }
```

---
transition: slide-left
---

# Hash Table / Dictionaries in JS (pg.4)

```js
  // Insert or update
  set(key, value) {
    const index = this.hash(key);
    const bucket = this.buckets[index];

    // Check if key already exists
    for (let pair of bucket) {
      if (pair[0] === key) {
        pair[1] = value; // update value
        return;
      }
    }

    // If key doesn't exist, insert new pair
    bucket.push([key, value]);
  }
```

---
transition: slide-left
---

# Hash Table / Dictionaries in JS (pg.5)

```js
  // Retrieve
  get(key) {
    const index = this.hash(key);
    const bucket = this.buckets[index];

    for (let pair of bucket) {
      if (pair[0] === key) {
        return pair[1];
      }
    }
    return undefined; // not found
  }
```

---
transition: slide-left
---

# Hash Table / Dictionaries in JS (pg.6)

```js
  // Remove
  remove(key) {
    const index = this.hash(key);
    const bucket = this.buckets[index];

    for (let i = 0; i < bucket.length; i++) {
      if (bucket[i][0] === key) {
        bucket.splice(i, 1);
        return true;
      }
    }
    return false;
  }

  // Print table (for testing)
  print() {
    this.buckets.forEach((bucket, i) => {
      if (bucket.length > 0) {
        console.log(`Bucket ${i}:`, bucket);
      }
    });
  }
}
```

---
layout: image-right
transition: slide-left
image: /assets/addy.png
backgroundSize: 400px 300px
class: text-left
---

# 10 minute break

🍦 Cool Tips, Trends and Resources:
- 🖇️ [Linked Lists](https://www.geeksforgeeks.org/linked-list-data-structure/)
- 👩‍💻 [NeetCode](https://www.freecodecamp.org/news/prepare-for-technical-interviews-using-neetcode-150)
- ➿ [Recursion](https://dev.to/codeguppy/recursion-in-javascript-practical-exercises-41hg)
- [Visual Go](https://visualgo.net/en)
- [Data Structure Visualization](https://www.cs.usfca.edu/~galles/visualization/Algorithms.html)
- [napkin ai](https://www.napkin.ai/)

<br>
<hr>
<br>

- 🧪 [Enter anonymous lab questions](https://docs.google.com/forms/d/e/1FAIpQLSevvGARdHQikso-uLqFCO481MABKE5HofuSrlzEPMNQ2ZLykw/viewform?usp=dialog)
- ℹ️ [Course feedback survey](https://circuitstream.typeform.com/to/ZoyYk7px#course_id=SoftwareAN&instructor=9514)

---
transition: slide-left
---

# Recursion

- A function that calls itself to solve a problem by breaking it down into smaller subproblems
- Each call brings us closer to a base case, which is a condition that stops the recursion
- Example: Demo Factorial function in [Loupe](http://latentflip.com/loupe/) (Note: functions are paused in call stack until the base case is reached)

<img src="/assets/recursion2.png" width="400" style="display: block; margin: 0 auto"/>

<!-->
- function factorial(n) {
- if (n === 0 || n === 1) return 1; // Base case
- return n * factorial(n - 1); // Recursive call
- }
- console.log(factorial(3)); // Output: 120
-->

---
transition: slide-left
---

# Why Recursion?

- Reduces complex problems into simpler, more elegant ones
- Helps solve naturally recursive problems (like tree traversal, backtracking, divide-and-conquer)
- Often cleaner and more elegant than loops
- Expected Computer Science knowledge (especially for interviews)
- Every recursive function must have:

| Part           | Purpose                             |
| -------------- | ----------------------------------- |
| Base case(s)      | Stops the recursion                 |
| Recursive case | Continues breaking down the problem |

Q: How is recursion different from iteration/loops?

---
transition: slide-left
---

# Iterative vs Recursive

<img src="/assets/recursion.png" width="700"/>

---
transition: slide-left
---

# Tips to Think About When Writing Recursive Functions

- Use a base case to stop recursion
- Think about how to break down the problem into smaller subproblems
- Just before you recurse, perhaps do-some-operation in addition to the result of the recursive call.  Example, note the `n *` portion of  `return n * factorial(n - 1)`


---
transition: slide-left
---

# Exercises: Recursion
Write recursive functions for the following problems.  Try not to use ChatGPT or Google to find the answers.

1. Write a function that computes: n to the exponent x
   - ex: `power(2, 3)` // should output 8
2. Calculate the sum of natural number up to n
   - ex: `sum(5) // should output 15`
3. Write a function that computes the nth Fibonacci number (1, 1, 2, 3, 5, 8, ...)
   - ex: `fibonacci(5) // should output 5`
4. Write a function that reverses a string
   - ex: `reverse("hello") // should output "olleh"`
5. Write a function that checks if a string is a palindrome (reads the same forwards and backwards)
   - ex: `isPalindrome("racecar") // should output true`

Writing Recursive functions can be challenging, so take your time and think through the problem.



---
transition: slide-left
---

# Homework

- Work on your "Note-taking" midterm app due June 15 midnight EST
   - can submit before due date if you wish
- Recursion exercises: https://leetcode.com/problem-list/recursion/