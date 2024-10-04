# 🌟 Data Structures Compendium in Python 🌟

Welcome to the comprehensive guide to Data Structures! This repository serves as an extensive resource for understanding, implementing, and mastering various data structures crucial to computer science and software engineering.

## 📚 Table of Contents

- [🌟 Data Structures Compendium in Python 🌟](#-data-structures-compendium-in-python-)
  - [📚 Table of Contents](#-table-of-contents)
  - [Introduction to Data Structures](#introduction-to-data-structures)
  - [Linear Data Structures](#linear-data-structures)
    - [Arrays](#arrays)
    - [Linked Lists](#linked-lists)
    - [Stacks](#stacks)
    - [Queues](#queues)
  - [Non-Linear Data Structures](#non-linear-data-structures)
    - [Trees](#trees)
    - [Graphs](#graphs)
    - [Heaps](#heaps)
  - [Hash-Based Structures](#hash-based-structures)
    - [Hash Tables](#hash-tables)
  - [Advanced Data Structures](#advanced-data-structures)
    - [Trie](#trie)
    - [Segment Tree](#segment-tree)
    - [Fenwick Tree (Binary Indexed Tree)](#fenwick-tree-binary-indexed-tree)
    - [Disjoint Set (Union-Find)](#disjoint-set-union-find)
  - [Time and Space Complexity](#time-and-space-complexity)
  - [Choosing the Right Data Structure](#choosing-the-right-data-structure)
  - [Contributing](#contributing)
  - [License](#license)

## Introduction to Data Structures

Data structures are specialized formats for organizing, processing, retrieving, and storing data. They provide a way to manage large amounts of data efficiently for uses such as large databases and internet indexing services. The choice of the appropriate data structure often leads to more efficient algorithms.

## Linear Data Structures

### Arrays

Arrays are the simplest and most widely used data structures. They store elements in contiguous memory locations, allowing for constant-time access to elements via their indices.

Types of Arrays:

1. Static Arrays: Fixed-size arrays
2. Dynamic Arrays: Resizable arrays (e.g., ArrayList in Java, vector in C++)

Key Operations:

- Access: O(1)
- Search: O(n) for unsorted, O(log n) for sorted (using binary search)
- Insertion: O(n) (worst case, when inserting at the beginning)
- Deletion: O(n) (worst case, when deleting from the beginning)

Example implementation (Dynamic Array in Python):

```python
class DynamicArray:
    def __init__(self):
        self.size = 0
        self.capacity = 1
        self.array = self.make_array(self.capacity)

    def __len__(self):
        return self.size

    def __getitem__(self, index):
        if not 0 <= index < self.size:
            raise IndexError('Index out of bounds')
        return self.array[index]

    def append(self, element):
        if self.size == self.capacity:
            self._resize(2 * self.capacity)
        self.array[self.size] = element
        self.size += 1

    def _resize(self, new_capacity):
        new_array = self.make_array(new_capacity)
        for i in range(self.size):
            new_array[i] = self.array[i]
        self.array = new_array
        self.capacity = new_capacity

    def make_array(self, capacity):
        return [None] * capacity
```

### Linked Lists

Linked Lists consist of nodes, where each node contains data and a reference (or link) to the next node in the sequence.

Types of Linked Lists:

1. Singly Linked List: Each node points to the next node
2. Doubly Linked List: Each node has pointers to both the next and previous nodes
3. Circular Linked List: The last node points back to the first node

Key Operations:

- Access: O(n)
- Search: O(n)
- Insertion: O(1) (if position is known)
- Deletion: O(1) (if position is known)

Example implementation (Singly Linked List in Python):

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class SinglyLinkedList:
    def __init__(self):
        self.head = None

    def append(self, data):
        new_node = Node(data)
        if not self.head:
            self.head = new_node
            return
        current = self.head
        while current.next:
            current = current.next
        current.next = new_node

    def delete(self, data):
        if not self.head:
            return
        if self.head.data == data:
            self.head = self.head.next
            return
        current = self.head
        while current.next:
            if current.next.data == data:
                current.next = current.next.next
                return
            current = current.next
```

### Stacks

Stacks follow the Last-In-First-Out (LIFO) principle. The last element added to the stack will be the first one to be removed.

Key Operations:

- Push: O(1)
- Pop: O(1)
- Peek (Top): O(1)

Example implementation (Stack using a Python list):

```python
class Stack:
    def __init__(self):
        self.items = []

    def is_empty(self):
        return len(self.items) == 0

    def push(self, item):
        self.items.append(item)

    def pop(self):
        if not self.is_empty():
            return self.items.pop()

    def peek(self):
        if not self.is_empty():
            return self.items[-1]

    def size(self):
        return len(self.items)
```

### Queues

Queues follow the First-In-First-Out (FIFO) principle. The first element added to the queue will be the first one to be removed.

Types of Queues:

1. Simple Queue
2. Circular Queue
3. Priority Queue
4. Double-Ended Queue (Deque)

Key Operations:

- Enqueue: O(1)
- Dequeue: O(1)
- Front: O(1)
- Rear: O(1)

Example implementation (Queue using a Python list):

```python
class Queue:
    def __init__(self):
        self.items = []

    def is_empty(self):
        return len(self.items) == 0

    def enqueue(self, item):
        self.items.append(item)

    def dequeue(self):
        if not self.is_empty():
            return self.items.pop(0)

    def front(self):
        if not self.is_empty():
            return self.items[0]

    def rear(self):
        if not self.is_empty():
            return self.items[-1]

    def size(self):
        return len(self.items)
```

## Non-Linear Data Structures

### Trees

Trees are hierarchical data structures consisting of nodes connected by edges. Each tree has a root node, and every node has zero or more child nodes.

Types of Trees:

1. Binary Tree: Each node has at most two children
2. Binary Search Tree (BST): A binary tree where left child < parent < right child
3. AVL Tree: Self-balancing BST
4. Red-Black Tree: Self-balancing BST with one extra bit per node for color
5. B-Tree: Self-balancing tree data structure that maintains sorted data and allows searches, sequential access, insertions, and deletions in logarithmic time

Key Operations (for BST):

- Search: O(log n) average, O(n) worst
- Insertion: O(log n) average, O(n) worst
- Deletion: O(log n) average, O(n) worst

Example implementation (Binary Search Tree in Python):

```python
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

class BinarySearchTree:
    def __init__(self):
        self.root = None

    def insert(self, value):
        if not self.root:
            self.root = TreeNode(value)
        else:
            self._insert_recursive(self.root, value)

    def _insert_recursive(self, node, value):
        if value < node.value:
            if node.left is None:
                node.left = TreeNode(value)
            else:
                self._insert_recursive(node.left, value)
        else:
            if node.right is None:
                node.right = TreeNode(value)
            else:
                self._insert_recursive(node.right, value)

    def search(self, value):
        return self._search_recursive(self.root, value)

    def _search_recursive(self, node, value):
        if node is None or node.value == value:
            return node
        if value < node.value:
            return self._search_recursive(node.left, value)
        return self._search_recursive(node.right, value)
```

### Graphs

Graphs consist of vertices (nodes) and edges that connect these vertices. They are used to represent networks, relationships, and various other complex structures.

Types of Graphs:

1. Directed Graph (Digraph)
2. Undirected Graph
3. Weighted Graph
4. Unweighted Graph

Representations:

1. Adjacency Matrix
2. Adjacency List

Key Algorithms:

- Depth-First Search (DFS): O(V + E)
- Breadth-First Search (BFS): O(V + E)
- Dijkstra's Shortest Path: O((V + E) log V)
- Bellman-Ford Algorithm: O(VE)
- Floyd-Warshall Algorithm: O(V^3)
- Kruskal's Minimum Spanning Tree: O(E log E)
- Prim's Minimum Spanning Tree: O(E log V)

Example implementation (Graph using Adjacency List in Python):

```python
from collections import defaultdict

class Graph:
    def __init__(self):
        self.graph = defaultdict(list)

    def add_edge(self, u, v):
        self.graph[u].append(v)

    def bfs(self, start):
        visited = set()
        queue = [start]
        visited.add(start)

        while queue:
            vertex = queue.pop(0)
            print(vertex, end=" ")

            for neighbor in self.graph[vertex]:
                if neighbor not in visited:
                    visited.add(neighbor)
                    queue.append(neighbor)

    def dfs(self, start):
        visited = set()
        self._dfs_recursive(start, visited)

    def _dfs_recursive(self, vertex, visited):
        visited.add(vertex)
        print(vertex, end=" ")

        for neighbor in self.graph[vertex]:
            if neighbor not in visited:
                self._dfs_recursive(neighbor, visited)
```

### Heaps

Heaps are specialized tree-based data structures that satisfy the heap property. In a max heap, for any given node, the node's value is greater than or equal to the values of its children. In a min heap, the node's value is less than or equal to the values of its children.

Types of Heaps:

1. Binary Heap
2. Fibonacci Heap
3. Binomial Heap

Key Operations:

- Insert: O(log n)
- Delete max/min: O(log n)
- Get max/min: O(1)
- Heapify: O(n)

Example implementation (Binary Max Heap in Python):

```python
class MaxHeap:
    def __init__(self):
        self.heap = []

    def parent(self, i):
        return (i - 1) // 2

    def left_child(self, i):
        return 2 * i + 1

    def right_child(self, i):
        return 2 * i + 2

    def swap(self, i, j):
        self.heap[i], self.heap[j] = self.heap[j], self.heap[i]

    def insert(self, key):
        self.heap.append(key)
        self._heapify_up(len(self.heap) - 1)

    def _heapify_up(self, i):
        parent = self.parent(i)
        if i > 0 and self.heap[i] > self.heap[parent]:
            self.swap(i, parent)
            self._heapify_up(parent)

    def extract_max(self):
        if len(self.heap) == 0:
            return None
        if len(self.heap) == 1:
            return self.heap.pop()

        max_val = self.heap[0]
        self.heap[0] = self.heap.pop()
        self._heapify_down(0)

        return max_val

    def _heapify_down(self, i):
        max_index = i
        left = self.left_child(i)
        right = self.right_child(i)

        if left < len(self.heap) and self.heap[left] > self.heap[max_index]:
            max_index = left

        if right < len(self.heap) and self.heap[right] > self.heap[max_index]:
            max_index = right

        if i != max_index:
            self.swap(i, max_index)
            self._heapify_down(max_index)
```

## Hash-Based Structures

### Hash Tables

Hash tables are data structures that implement an associative array abstract data type, a structure that can map keys to values. They use a hash function to compute an index into an array of buckets or slots, from which the desired value can be found.

Key Operations:

- Insert: O(1) average, O(n) worst
- Delete: O(1) average, O(n) worst
- Search: O(1) average, O(n) worst

Example implementation (Hash Table with chaining in Python):

```python
class HashNode:
    def __init__(self, key, value):
        self.key = key
        self.value = value
        self.next = None

class HashTable:
    def __init__(self, size):
        self.size = size
        self.table = [None] * size

    def _hash(self, key):
        return hash(key) % self.size

    def insert(self, key, value):
        index = self._hash(key)
        if self.table[index] is None:
            self.table[index] = HashNode(key, value)
        else:
            current = self.table[index]
            while current:
                if current.key == key:
                    current.value = value
                    return
                if current.next is None:
                    break
                current = current.next
            current.next = HashNode(key, value)

    def get(self, key):
        index = self._hash(key)
        current = self.table[index]
        while current:
            if current.key == key:
                return current.value
            current = current.next
        raise KeyError(key)

    def remove(self, key):
        index = self._hash(key)
        if self.table[index] is None:
            raise KeyError(key)
        if self.table[index].key == key:
            self.table[index] = self.table[index].next
            return
        current = self.table[index]
        while current.next:
            if current.next.key == key:
                current.next = current.next.next
            return
            current = current.next
        raise KeyError(key)
```

## Advanced Data Structures

### Trie

A Trie, also called a prefix tree, is a tree-like data structure used to store and retrieve strings. It's particularly useful for tasks involving string prefixes, such as autocomplete and spell checking.

Key Operations:

- Insert: O(m), where m is the length of the string
- Search: O(m)
- Delete: O(m)

Example implementation (Trie in Python):

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end_of_word = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end_of_word = True

    def search(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
        return node.is_end_of_word

    def starts_with(self, prefix):
        node = self.root
        for char in prefix:
            if char not in node.children:
                return False
            node = node.children[char]
        return True
```

### Segment Tree

A Segment Tree is a tree data structure used for storing information about intervals, or segments. It allows for efficient query operations over an array or list, especially for range queries.

Key Operations:

- Build: O(n)
- Query: O(log n)
- Update: O(log n)

Example implementation (Segment Tree for range sum queries in Python):

```python
class SegmentTree:
    def __init__(self, arr):
        self.n = len(arr)
        self.tree = [0] * (4 * self.n)
        self._build(arr, 0, 0, self.n - 1)

    def _build(self, arr, v, tl, tr):
        if tl == tr:
            self.tree[v] = arr[tl]
        else:
            tm = (tl + tr) // 2
            self._build(arr, v*2+1, tl, tm)
            self._build(arr, v*2+2, tm+1, tr)
            self.tree[v] = self.tree[v*2+1] + self.tree[v*2+2]

    def query(self, l, r):
        return self._query(0, 0, self.n - 1, l, r)

    def _query(self, v, tl, tr, l, r):
        if l > r:
            return 0
        if l == tl and r == tr:
            return self.tree[v]
        tm = (tl + tr) // 2
        return (self._query(v*2+1, tl, tm, l, min(r, tm))
                + self._query(v*2+2, tm+1, tr, max(l, tm+1), r))

    def update(self, pos, new_val):
        self._update(0, 0, self.n - 1, pos, new_val)

    def _update(self, v, tl, tr, pos, new_val):
        if tl == tr:
            self.tree[v] = new_val
        else:
            tm = (tl + tr) // 2
            if pos <= tm:
                self._update(v*2+1, tl, tm, pos, new_val)
            else:
                self._update(v*2+2, tm+1, tr, pos, new_val)
            self.tree[v] = self.tree[v*2+1] + self.tree[v*2+2]
```

### Fenwick Tree (Binary Indexed Tree)

A Fenwick Tree, also known as a Binary Indexed Tree, is a data structure that can efficiently update elements and calculate prefix sums in a table of numbers.

Key Operations:

- Update: O(log n)
- Query (Prefix Sum): O(log n)

Example implementation (Fenwick Tree in Python):

```python
class FenwickTree:
    def __init__(self, n):
        self.size = n
        self.tree = [0] * (n + 1)

    def update(self, i, delta):
        while i <= self.size:
            self.tree[i] += delta
            i += i & (-i)

    def query(self, i):
        sum = 0
        while i > 0:
            sum += self.tree[i]
            i -= i & (-i)
        return sum

    def range_query(self, left, right):
        return self.query(right) - self.query(left - 1)
```

### Disjoint Set (Union-Find)

A Disjoint Set data structure, also known as Union-Find, keeps track of a set of elements partitioned into a number of disjoint (non-overlapping) subsets.

Key Operations:

- Find: O(α(n)), where α is the inverse Ackermann function
- Union: O(α(n))

Example implementation (Disjoint Set with path compression and union by rank in Python):

```python
class DisjointSet:
    def __init__(self, n):
        self.parent = list(range(n))
        self.rank = [0] * n

    def find(self, item):
        if self.parent[item] != item:
            self.parent[item] = self.find(self.parent[item])
        return self.parent[item]

    def union(self, set1, set2):
        root1 = self.find(set1)
        root2 = self.find(set2)

        if root1 != root2:
            if self.rank[root1] < self.rank[root2]:
                self.parent[root1] = root2
            elif self.rank[root1] > self.rank[root2]:
                self.parent[root2] = root1
            else:
                self.parent[root2] = root1
                self.rank[root1] += 1
```

## Time and Space Complexity

Understanding the time and space complexity of data structures is crucial for choosing the right one for a specific problem. Here's a summary of the big O notation for common operations on various data structures:

| Data Structure     | Access     | Search     | Insertion  | Deletion   | Space     |
| ------------------ | ---------- | ---------- | ---------- | ---------- | --------- |
| Array              | O(1)       | O(n)       | O(n)       | O(n)       | O(n)      |
| Linked List        | O(n)       | O(n)       | O(1)       | O(1)       | O(n)      |
| Stack              | O(n)       | O(n)       | O(1)       | O(1)       | O(n)      |
| Queue              | O(n)       | O(n)       | O(1)       | O(1)       | O(n)      |
| Hash Table         | N/A        | O(1)\*     | O(1)\*     | O(1)\*     | O(n)      |
| Binary Search Tree | O(log n)\* | O(log n)\* | O(log n)\* | O(log n)\* | O(n)      |
| AVL Tree           | O(log n)   | O(log n)   | O(log n)   | O(log n)   | O(n)      |
| B-Tree             | O(log n)   | O(log n)   | O(log n)   | O(log n)   | O(n)      |
| Red-Black Tree     | O(log n)   | O(log n)   | O(log n)   | O(log n)   | O(n)      |
| Heap               | N/A        | O(n)       | O(log n)   | O(log n)   | O(n)      |
| Trie               | O(k)       | O(k)       | O(k)       | O(k)       | O(n \* k) |

\*Note: Average case. Worst case may be different.

## Choosing the Right Data Structure

Selecting the appropriate data structure depends on various factors:

1. Nature of the problem: Understand the operations you'll be performing most frequently.
2. Time complexity: Consider the efficiency of common operations for your use case.
3. Space complexity: Evaluate the memory requirements of the data structure.
4. Ease of implementation: Sometimes, a simpler structure might be preferable if it meets the performance requirements.

Here are some general guidelines:

- Use arrays for simple, fixed-size collections with fast access by index.
- Choose linked lists for frequent insertions and deletions, especially at the beginning or end.
- Implement stacks for last-in-first-out (LIFO) scenarios, like undo mechanisms or parsing expressions.
- Use queues for first-in-first-out (FIFO) scenarios, such as breadth-first search or handling asynchronous requests.
- Apply hash tables for fast lookups, insertions, and deletions when you have a good hash function.
- Utilize trees (BST, AVL, Red-Black) for hierarchical data and when you need a sorted structure with efficient operations.
- Implement heaps for priority queue operations, like finding the minimum or maximum efficiently.
- Use tries for prefix matching and autocomplete features in string-based applications.
- Apply graph data structures for representing networks, relationships, or any interconnected data.

Remember, the best data structure often depends on the specific requirements of your problem and the constraints of your system.

## Contributing

We welcome contributions to this Data Structures repository! Here's how you can contribute:

1. Fork the repository
2. Create a new branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

Please make sure to update tests as appropriate and adhere to the existing coding style.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

---

We hope this comprehensive guide to data structures helps you in your journey to becoming a better programmer and computer scientist. Happy coding!
