# 🌟 Data Structures Compendium in Java 🌟

Welcome to the comprehensive guide to Data Structures implemented in Java! This repository serves as an extensive resource for understanding, implementing, and mastering various data structures crucial to computer science and software engineering.

## 📚 Table of Contents

- [🌟 Data Structures Compendium in Java 🌟](#-data-structures-compendium-in-java-)
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
2. Dynamic Arrays: Resizable arrays (e.g., ArrayList in Java)

Key Operations:
- Access: O(1)
- Search: O(n) for unsorted, O(log n) for sorted (using binary search)
- Insertion: O(n) (worst case, when inserting at the beginning)
- Deletion: O(n) (worst case, when deleting from the beginning)

Example implementation (Dynamic Array in Java):

```java
import java.util.Arrays;

public class DynamicArray<T> {
    private T[] array;
    private int size;
    private int capacity;

    @SuppressWarnings("unchecked")
    public DynamicArray() {
        array = (T[]) new Object[1];
        size = 0;
        capacity = 1;
    }

    public void add(T element) {
        if (size == capacity) {
            resize(2 * capacity);
        }
        array[size++] = element;
    }

    public T get(int index) {
        if (index < 0 || index >= size) {
            throw new IndexOutOfBoundsException("Index out of bounds");
        }
        return array[index];
    }

    public int size() {
        return size;
    }

    private void resize(int newCapacity) {
        array = Arrays.copyOf(array, newCapacity);
        capacity = newCapacity;
    }
}
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

Example implementation (Singly Linked List in Java):

```java
public class SinglyLinkedList<T> {
    private class Node {
        T data;
        Node next;

        Node(T data) {
            this.data = data;
            this.next = null;
        }
    }

    private Node head;

    public void append(T data) {
        Node newNode = new Node(data);
        if (head == null) {
            head = newNode;
            return;
        }
        Node current = head;
        while (current.next != null) {
            current = current.next;
        }
        current.next = newNode;
    }

    public void delete(T data) {
        if (head == null) return;
        if (head.data.equals(data)) {
            head = head.next;
            return;
        }
        Node current = head;
        while (current.next != null && !current.next.data.equals(data)) {
            current = current.next;
        }
        if (current.next != null) {
            current.next = current.next.next;
        }
    }
}
```

### Stacks

Stacks follow the Last-In-First-Out (LIFO) principle. The last element added to the stack will be the first one to be removed.

Key Operations:
- Push: O(1)
- Pop: O(1)
- Peek (Top): O(1)

Example implementation (Stack using Java ArrayList):

```java
import java.util.ArrayList;

public class Stack<T> {
    private ArrayList<T> items;

    public Stack() {
        items = new ArrayList<>();
    }

    public boolean isEmpty() {
        return items.isEmpty();
    }

    public void push(T item) {
        items.add(item);
    }

    public T pop() {
        if (isEmpty()) {
            throw new IllegalStateException("Stack is empty");
        }
        return items.remove(items.size() - 1);
    }

    public T peek() {
        if (isEmpty()) {
            throw new IllegalStateException("Stack is empty");
        }
        return items.get(items.size() - 1);
    }

    public int size() {
        return items.size();
    }
}
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

Example implementation (Queue using Java LinkedList):

```java
import java.util.LinkedList;

public class Queue<T> {
    private LinkedList<T> items;

    public Queue() {
        items = new LinkedList<>();
    }

    public boolean isEmpty() {
        return items.isEmpty();
    }

    public void enqueue(T item) {
        items.addLast(item);
    }

    public T dequeue() {
        if (isEmpty()) {
            throw new IllegalStateException("Queue is empty");
        }
        return items.removeFirst();
    }

    public T front() {
        if (isEmpty()) {
            throw new IllegalStateException("Queue is empty");
        }
        return items.getFirst();
    }

    public T rear() {
        if (isEmpty()) {
            throw new IllegalStateException("Queue is empty");
        }
        return items.getLast();
    }

    public int size() {
        return items.size();
    }
}
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

Example implementation (Binary Search Tree in Java):

```java
public class BinarySearchTree<T extends Comparable<T>> {
    private class Node {
        T value;
        Node left, right;

        Node(T value) {
            this.value = value;
            left = right = null;
        }
    }

    private Node root;

    public void insert(T value) {
        root = insertRec(root, value);
    }

    private Node insertRec(Node root, T value) {
        if (root == null) {
            root = new Node(value);
            return root;
        }

        if (value.compareTo(root.value) < 0)
            root.left = insertRec(root.left, value);
        else if (value.compareTo(root.value) > 0)
            root.right = insertRec(root.right, value);

        return root;
    }

    public boolean search(T value) {
        return searchRec(root, value);
    }

    private boolean searchRec(Node root, T value) {
        if (root == null || root.value.equals(value))
            return root != null;

        if (value.compareTo(root.value) < 0)
            return searchRec(root.left, value);

        return searchRec(root.right, value);
    }
}
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

Example implementation (Graph using Adjacency List in Java):

```java
import java.util.*;

public class Graph {
    private Map<Integer, List<Integer>> adjacencyList;

    public Graph() {
        adjacencyList = new HashMap<>();
    }

    public void addEdge(int u, int v) {
        adjacencyList.computeIfAbsent(u, k -> new ArrayList<>()).add(v);
    }

    public void bfs(int start) {
        Set<Integer> visited = new HashSet<>();
        Queue<Integer> queue = new LinkedList<>();

        visited.add(start);
        queue.offer(start);

        while (!queue.isEmpty()) {
            int vertex = queue.poll();
            System.out.print(vertex + " ");

            List<Integer> neighbors = adjacencyList.getOrDefault(vertex, new ArrayList<>());
            for (int neighbor : neighbors) {
                if (!visited.contains(neighbor)) {
                    visited.add(neighbor);
                    queue.offer(neighbor);
                }
            }
        }
    }

    public void dfs(int start) {
        Set<Integer> visited = new HashSet<>();
        dfsRecursive(start, visited);
    }

    private void dfsRecursive(int vertex, Set<Integer> visited) {
        visited.add(vertex);
        System.out.print(vertex + " ");

        List<Integer> neighbors = adjacencyList.getOrDefault(vertex, new ArrayList<>());
        for (int neighbor : neighbors) {
            if (!visited.contains(neighbor)) {
                dfsRecursive(neighbor, visited);
            }
        }
    }
}
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

Example implementation (Binary Max Heap in Java):

```java
import java.util.ArrayList;
import java.util.List;

public class MaxHeap<T extends Comparable<T>> {
    private List<T> heap;

    public MaxHeap() {
        heap = new ArrayList<>();
    }

    private int parent(int i) {
        return (i - 1) / 2;
    }

    private int leftChild(int i) {
        return 2 * i + 1;
    }

    private int rightChild(int i) {
        return 2 * i + 2;
    }

    private void swap(int i, int j) {
        T temp = heap.get(i);
        heap.set(i, heap.get(j));
        heap.set(j, temp);
    }

    public void insert(T key) {
        heap.add(key);
        heapifyUp(heap.size() - 1);
    }

    private void heapifyUp(int i) {
        int parent = parent(i);
        if (i > 0 && heap.get(i).compareTo(heap.get(parent)) > 0) {
            swap(i, parent);
            heapifyUp(parent);
        }
    }

    public T extractMax() {
        if (heap.isEmpty()) {
            throw new IllegalStateException("Heap is empty");
        }
        if (heap.size() == 1) {
            return heap.remove(0);
        }

        T max = heap.get(0);
        heap.set(0, heap.remove(heap.size() - 1));
        heapifyDown(0);

        return max;
    }

    private void heapifyDown(int i) {
        int maxIndex = i;
        int left = leftChild(i);
        int right = rightChild(i);

        if (left < heap.size() && heap.get(left).compareTo(heap.get(maxIndex)) > 0) {
            maxIndex = left;
        }

        if (right < heap.size() && heap.get(right).compareTo(heap.get(maxIndex)) > 0) {
            maxIndex = right;
        }

        if (i != maxIndex) {
            swap(i, maxIndex);
            heapifyDown(maxIndex);
        }
    }
}
```

## Hash-Based Structures

### Hash Tables

Hash tables are data structures that implement an associative array abstract data type, a structure that can map keys to values. They use a hash function to compute an index into an array of buckets or slots, from which the desired value can be found.

Key Operations:
- Insert: O(1) average, O(n) worst
- Delete: O(1) average, O(n) worst
- Search: O(1) average, O(n) worst

Example implementation (Hash Table with chaining in Java):

```java
import java.util.LinkedList;

public class HashTable<K, V> {
    private static class HashNode<K, V> {
        K key;
        V value;
        HashNode<K, V> next;

        public HashNode(K key, V value) {
            this.key = key;
            this.value = value;
        }
    }

    private LinkedList<HashNode<K, V>>[] buckets;
    private int numBuckets;
    private int size;

    public HashTable() {
        this(10);
    }

    @SuppressWarnings("unchecked")
    public HashTable(int capacity) {
        buckets = new LinkedList[capacity];
        numBuckets = capacity;
        size = 0;
        for (int i = 0; i < capacity; i++) {
            buckets[i] = new LinkedList<>();
        }
    }

    private int getBucketIndex(K key) {
        int hashCode = key.hashCode();
        return Math.abs(hashCode) % numBuckets;
    }

    public void put(K key, V value) {
        int bucketIndex = getBucketIndex(key);
        LinkedList<HashNode<K, V>> bucket = buckets[bucketIndex];
        for (HashNode<K, V> node : bucket) {
            if (node.key.equals(key)) {
                node.value = value;
                return;
            }
        }
        bucket.add(new HashNode<>(key, value));
        size++;

        if ((1.0 * size) / numBuckets >= 0.7) {
            resize();
        }
    }

    public V get(K key) {
        int bucketIndex = getBucketIndex(key);
        LinkedList<HashNode<K, V>> bucket = buckets[bucketIndex];
        for (HashNode<K, V> node : bucket) {
            if (node.key.equals(key)) {
                return node.value;
            }
        }
        return null;
    }

    public V remove(K key) {
        int bucketIndex = getBucketIndex(key);
        LinkedList<HashNode<K, V>> bucket = buckets[bucketIndex];
        HashNode<K, V> prev = null;
        for (HashNode<K, V> node : bucket) {
            if (node.key.equals(key)) {
                if (prev == null) {
                    bucket.removeFirst();
                } else {
                    prev.next = node.next;
                }
                size--;
                return node.value;
            }
            prev = node;
        }
        return null;
    }

    @SuppressWarnings("unchecked")
    private void resize() {
        LinkedList<HashNode<K, V>>[] oldBuckets = buckets;
        numBuckets *= 2;
        buckets = new LinkedList[numBuckets];
        for (int i = 0; i < numBuckets; i++) {
            buckets[i] = new LinkedList<>();
        }
        size = 0;
        for (LinkedList<HashNode<K, V>> bucket : oldBuckets) {
            for (HashNode<K, V> node : bucket) {
                put(node.key, node.value);
            }
        }
    }
}
```

## Advanced Data Structures

### Trie

A Trie, also called a prefix tree, is a tree-like data structure used to store and retrieve strings. It's particularly useful for tasks involving string prefixes, such as autocomplete and spell checking.

Key Operations:
- Insert: O(m), where m is the length of the string
- Search: O(m)
- Delete: O(m)

Example implementation (Trie in Java):

```java
import java.util.HashMap;
import java.util.Map;

public class Trie {
    private class TrieNode {
        Map<Character, TrieNode> children;
        boolean isEndOfWord;

        TrieNode() {
            children = new HashMap<>();
            isEndOfWord = false;
        }
    }

    private final TrieNode root;

    public Trie() {
        root = new TrieNode();
    }

    public void insert(String word) {
        TrieNode current = root;
        for (char ch : word.toCharArray()) {
            current = current.children.computeIfAbsent(ch, c -> new TrieNode());
        }
        current.isEndOfWord = true;
    }

    public boolean search(String word) {
        TrieNode node = searchPrefix(word);
        return node != null && node.isEndOfWord;
    }

    public boolean startsWith(String prefix) {
        return searchPrefix(prefix) != null;
    }

    private TrieNode searchPrefix(String prefix) {
        TrieNode current = root;
        for (char ch : prefix.toCharArray()) {
            TrieNode node = current.children.get(ch);
            if (node == null) {
                return null;
            }
            current = node;
        }
        return current;
    }
}
```

### Segment Tree

A Segment Tree is a tree data structure used for storing information about intervals, or segments. It allows for efficient query operations over an array or list, especially for range queries.

Key Operations:
- Build: O(n)
- Query: O(log n)
- Update: O(log n)

Example implementation (Segment Tree for range sum queries in Java):

```java
public class SegmentTree {
    private int[] tree;
    private int n;

    public SegmentTree(int[] arr) {
        n = arr.length;
        tree = new int[4 * n];
        buildTree(arr, 0, 0, n - 1);
    }

    private void buildTree(int[] arr, int v, int tl, int tr) {
        if (tl == tr) {
            tree[v] = arr[tl];
        } else {
            int tm = (tl + tr) / 2;
            buildTree(arr, v * 2 + 1, tl, tm);
            buildTree(arr, v * 2 + 2, tm + 1, tr);
            tree[v] = tree[v * 2 + 1] + tree[v * 2 + 2];
        }
    }

    public int query(int l, int r) {
        return query(0, 0, n - 1, l, r);
    }

    private int query(int v, int tl, int tr, int l, int r) {
        if (l > r) {
            return 0;
        }
        if (l == tl && r == tr) {
            return tree[v];
        }
        int tm = (tl + tr) / 2;
        return query(v * 2 + 1, tl, tm, l, Math.min(r, tm))
             + query(v * 2 + 2, tm + 1, tr, Math.max(l, tm + 1), r);
    }

    public void update(int pos, int newVal) {
        update(0, 0, n - 1, pos, newVal);
    }

    private void update(int v, int tl, int tr, int pos, int newVal) {
        if (tl == tr) {
            tree[v] = newVal;
        } else {
            int tm = (tl + tr) / 2;
            if (pos <= tm) {
                update(v * 2 + 1, tl, tm, pos, newVal);
            } else {
                update(v * 2 + 2, tm + 1, tr, pos, newVal);
            }
            tree[v] = tree[v * 2 + 1] + tree[v * 2 + 2];
        }
    }
}
```

### Fenwick Tree (Binary Indexed Tree)

A Fenwick Tree, also known as a Binary Indexed Tree, is a data structure that can efficiently update elements and calculate prefix sums in a table of numbers.

Key Operations:
- Update: O(log n)
- Query (Prefix Sum): O(log n)

Example implementation (Fenwick Tree in Java):

```java
public class FenwickTree {
    private int[] tree;

    public FenwickTree(int n) {
        tree = new int[n + 1];
    }

    public void update(int i, int delta) {
        while (i < tree.length) {
            tree[i] += delta;
            i += i & (-i);
        }
    }

    public int query(int i) {
        int sum = 0;
        while (i > 0) {
            sum += tree[i];
            i -= i & (-i);
        }
        return sum;
    }

    public int rangeQuery(int left, int right) {
        return query(right) - query(left - 1);
    }
}
```

### Disjoint Set (Union-Find)

A Disjoint Set data structure, also known as Union-Find, keeps track of a set of elements partitioned into a number of disjoint (non-overlapping) subsets.

Key Operations:
- Find: O(α(n)), where α is the inverse Ackermann function
- Union: O(α(n))

Example implementation (Disjoint Set with path compression and union by rank in Java):

```java
public class DisjointSet {
    private int[] parent;
    private int[] rank;

    public DisjointSet(int n) {
        parent = new int[n];
        rank = new int[n];
        for (int i = 0; i < n; i++) {
            parent[i] = i;
        }
    }

    public int find(int x) {
        if (parent[x] != x) {
            parent[x] = find(parent[x]);
        }
        return parent[x];
    }

    public void union(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);

        if (rootX != rootY) {
            if (rank[rootX] < rank[rootY]) {
                parent[rootX] = rootY;
            } else if (rank[rootX] > rank[rootY]) {
                parent[rootY] = rootX;
            } else {
                parent[rootY] = rootX;
                rank[rootX]++;
            }
        }
    }
}
```

## Time and Space Complexity

Understanding the time and space complexity of data structures is crucial for choosing the right one for a specific problem. Here's a summary of the big O notation for common operations on various data structures:

| Data Structure     | Access    | Search    | Insertion | Deletion  | Space    |
|--------------------|-----------|-----------|-----------|-----------|----------|
| Array              | O(1)      | O(n)      | O(n)      | O(n)      | O(n)     |
| Linked List        | O(n)      | O(n)      | O(1)      | O(1)      | O(n)     |
| Stack              | O(n)      | O(n)      | O(1)      | O(1)      | O(n)     |
| Queue              | O(n)      | O(n)      | O(1)      | O(1)      | O(n)     |
| Hash Table         | N/A       | O(1)*     | O(1)*     | O(1)*     | O(n)     |
| Binary Search Tree | O(log n)* | O(log n)* | O(log n)* | O(log n)* | O(n)     |
| AVL Tree           | O(log n)  | O(log n)  | O(log n)  | O(log n)  | O(n)     |
| B-Tree             | O(log n)  | O(log n)  | O(log n)  | O(log n)  | O(n)     |
| Red-Black Tree     | O(log n)  | O(log n)  | O(log n)  | O(log n)  | O(n)     |
| Heap               | N/A       | O(n)      | O(log n)  | O(log n)  | O(n)     |
| Trie               | O(k)      | O(k)      | O(k)      | O(k)      | O(n * k) |

*Note: Average case. Worst case may be different.

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

This project is licensed under the MIT License.

---

We hope this comprehensive guide to data structures in Java helps you in your journey to becoming a better programmer and computer scientist. Happy coding!