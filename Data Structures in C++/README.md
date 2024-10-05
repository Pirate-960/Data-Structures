# 🌟 Data Structures Compendium in C++ 🌟

Welcome to the comprehensive guide to Data Structures implemented in C++! This repository serves as an extensive resource for understanding, implementing, and mastering various data structures crucial to computer science and software engineering.

## 📚 Table of Contents

- [🌟 Data Structures Compendium in C++ 🌟](#-data-structures-compendium-in-c-)
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
2. Dynamic Arrays: Resizable arrays (e.g., std::vector in C++)

Key Operations:
- Access: O(1)
- Search: O(n) for unsorted, O(log n) for sorted (using binary search)
- Insertion: O(n) (worst case, when inserting at the beginning)
- Deletion: O(n) (worst case, when deleting from the beginning)

Example implementation (Dynamic Array in C++):

```cpp
#include <iostream>
#include <stdexcept>

template <typename T>
class DynamicArray {
private:
    T* array;
    int size;
    int capacity;

    void resize(int newCapacity) {
        T* newArray = new T[newCapacity];
        for (int i = 0; i < size; i++) {
            newArray[i] = array[i];
        }
        delete[] array;
        array = newArray;
        capacity = newCapacity;
    }

public:
    DynamicArray() : array(new T[1]), size(0), capacity(1) {}

    ~DynamicArray() {
        delete[] array;
    }

    void add(T element) {
        if (size == capacity) {
            resize(2 * capacity);
        }
        array[size++] = element;
    }

    T get(int index) const {
        if (index < 0 || index >= size) {
            throw std::out_of_range("Index out of bounds");
        }
        return array[index];
    }

    int getSize() const {
        return size;
    }
};
```

### Linked Lists

Linked Lists consist of nodes, where each node contains data and a pointer (or link) to the next node in the sequence.

Types of Linked Lists:
1. Singly Linked List: Each node points to the next node
2. Doubly Linked List: Each node has pointers to both the next and previous nodes
3. Circular Linked List: The last node points back to the first node

Key Operations:
- Access: O(n)
- Search: O(n)
- Insertion: O(1) (if position is known)
- Deletion: O(1) (if position is known)

Example implementation (Singly Linked List in C++):

```cpp
#include <iostream>

template <typename T>
class SinglyLinkedList {
private:
    struct Node {
        T data;
        Node* next;
        Node(T data) : data(data), next(nullptr) {}
    };

    Node* head;

public:
    SinglyLinkedList() : head(nullptr) {}

    void append(T data) {
        Node* newNode = new Node(data);
        if (head == nullptr) {
            head = newNode;
            return;
        }
        Node* current = head;
        while (current->next != nullptr) {
            current = current->next;
        }
        current->next = newNode;
    }

    void remove(T data) {
        if (head == nullptr) return;
        if (head->data == data) {
            Node* temp = head;
            head = head->next;
            delete temp;
            return;
        }
        Node* current = head;
        while (current->next != nullptr && current->next->data != data) {
            current = current->next;
        }
        if (current->next != nullptr) {
            Node* temp = current->next;
            current->next = current->next->next;
            delete temp;
        }
    }

    ~SinglyLinkedList() {
        while (head != nullptr) {
            Node* temp = head;
            head = head->next;
            delete temp;
        }
    }
};
```

### Stacks

Stacks follow the Last-In-First-Out (LIFO) principle. The last element added to the stack will be the first one to be removed.

Key Operations:
- Push: O(1)
- Pop: O(1)
- Top: O(1)

Example implementation (Stack using C++ std::vector):

```cpp
#include <vector>
#include <stdexcept>

template <typename T>
class Stack {
private:
    std::vector<T> items;

public:
    bool isEmpty() const {
        return items.empty();
    }

    void push(T item) {
        items.push_back(item);
    }

    T pop() {
        if (isEmpty()) {
            throw std::runtime_error("Stack is empty");
        }
        T item = items.back();
        items.pop_back();
        return item;
    }

    T top() const {
        if (isEmpty()) {
            throw std::runtime_error("Stack is empty");
        }
        return items.back();
    }

    int size() const {
        return items.size();
    }
};
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

Example implementation (Queue using C++ std::deque):

```cpp
#include <deque>
#include <stdexcept>

template <typename T>
class Queue {
private:
    std::deque<T> items;

public:
    bool isEmpty() const {
        return items.empty();
    }

    void enqueue(T item) {
        items.push_back(item);
    }

    T dequeue() {
        if (isEmpty()) {
            throw std::runtime_error("Queue is empty");
        }
        T item = items.front();
        items.pop_front();
        return item;
    }

    T front() const {
        if (isEmpty()) {
            throw std::runtime_error("Queue is empty");
        }
        return items.front();
    }

    T rear() const {
        if (isEmpty()) {
            throw std::runtime_error("Queue is empty");
        }
        return items.back();
    }

    int size() const {
        return items.size();
    }
};
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

Example implementation (Binary Search Tree in C++):

```cpp
#include <iostream>

template <typename T>
class BinarySearchTree {
private:
    struct Node {
        T value;
        Node* left;
        Node* right;
        Node(T value) : value(value), left(nullptr), right(nullptr) {}
    };

    Node* root;

    Node* insertRec(Node* root, T value) {
        if (root == nullptr) {
            return new Node(value);
        }

        if (value < root->value) {
            root->left = insertRec(root->left, value);
        } else if (value > root->value) {
            root->right = insertRec(root->right, value);
        }

        return root;
    }

    bool searchRec(Node* root, T value) const {
        if (root == nullptr || root->value == value) {
            return root != nullptr;
        }

        if (value < root->value) {
            return searchRec(root->left, value);
        }

        return searchRec(root->right, value);
    }

    void deleteTree(Node* node) {
        if (node == nullptr) return;
        deleteTree(node->left);
        deleteTree(node->right);
        delete node;
    }

public:
    BinarySearchTree() : root(nullptr) {}

    void insert(T value) {
        root = insertRec(root, value);
    }

    bool search(T value) const {
        return searchRec(root, value);
    }

    ~BinarySearchTree() {
        deleteTree(root);
    }
};
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

Example implementation (Graph using Adjacency List in C++):

```cpp
#include <vector>
#include <list>
#include <queue>
#include <iostream>

class Graph {
private:
    int V;
    std::vector<std::list<int>> adjList;

public:
    Graph(int vertices) : V(vertices), adjList(vertices) {}

    void addEdge(int u, int v) {
        adjList[u].push_back(v);
    }

    void bfs(int start) {
        std::vector<bool> visited(V, false);
        std::queue<int> queue;

        visited[start] = true;
        queue.push(start);

        while (!queue.empty()) {
            int vertex = queue.front();
            queue.pop();
            std::cout << vertex << " ";

            for (int neighbor : adjList[vertex]) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.push(neighbor);
                }
            }
        }
    }

    void dfsUtil(int v, std::vector<bool>& visited) {
        visited[v] = true;
        std::cout << v << " ";

        for (int neighbor : adjList[v]) {
            if (!visited[neighbor]) {
                dfsUtil(neighbor, visited);
            }
        }
    }

    void dfs(int start) {
        std::vector<bool> visited(V, false);
        dfsUtil(start, visited);
    }
};
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

Example implementation (Binary Max Heap in C++):

```cpp
#include <vector>
#include <stdexcept>

template <typename T>
class MaxHeap {
private:
    std::vector<T> heap;

    int parent(int i) { return (i - 1) / 2; }
    int leftChild(int i) { return 2 * i + 1; }
    int rightChild(int i) { return 2 * i + 2; }

    void swap(int i, int j) {
        T temp = heap[i];
        heap[i] = heap[j];
        heap[j] = temp;
    }

    void heapifyUp(int i) {
        int p = parent(i);
        if (i > 0 && heap[i] > heap[p]) {
            swap(i, p);
            heapifyUp(p);
        }
    }

    void heapifyDown(int i) {
        int maxIndex = i;
        int left = leftChild(i);
        int right = rightChild(i);

        if (left < heap.size() && heap[left] > heap[maxIndex]) {
            maxIndex = left;
        }

        if (right < heap.size() && heap[right] > heap[maxIndex]) {
            maxIndex = right;
        }

        if (i != maxIndex) {
            swap(i, maxIndex);
            heapifyDown(maxIndex);
        }
    }

public:
    void insert(T key) {
        heap.push_back(key);
        heapifyUp(heap.size() - 1);
    }

    T extractMax() {
        if (heap.empty()) {
            throw std::runtime_error("Heap is empty");
        }
        if (heap.size() == 1) {
            T max = heap[0];
            heap.pop_back();
            return max;
        }

        T max = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        heapifyDown(0);

        return max;
    }
};
```

## Hash-Based Structures

### Hash Tables

Hash tables are data structures that implement an associative array abstract data type, a structure that can map keys to values. They use a hash function to compute an index into an array of buckets or slots, from which the desired value can be found.

Key Operations:
- Insert: O(1) average, O(n) worst
- Delete: O(1) average, O(n) worst
- Search: O(1) average, O(n) worst

Example implementation (Hash Table with chaining in C++):

```cpp
#include <vector>
#include <list>
#include <stdexcept>

template<typename K, typename V>
class HashTable {
private:
    struct HashNode {
        K key;
        V value;
        HashNode(K key, V value) : key(key), value(value) {}
    };

    std::vector<std::list<HashNode>> buckets;
    int numBuckets;
    int size;

    int getBucketIndex(K key) const {
        return std::hash<K>{}(key) % numBuckets;
    }

    void resize() {
        std::vector<std::list<HashNode>> oldBuckets = buckets;
        numBuckets *= 2;
        buckets.clear();
        buckets.resize(numBuckets);
        size = 0;

        for (const auto& bucket : oldBuckets) {
            for (const auto& node : bucket) {
                put(node.key, node.value);
            }
        }
    }

public:
    HashTable(int capacity = 10) : numBuckets(capacity), size(0) {
        buckets.resize(numBuckets);
    }

    void put(K key, V value) {
        int bucketIndex = getBucketIndex(key);
        auto& bucket = buckets[bucketIndex];

        for (auto& node : bucket) {
            if (node.key == key) {
                node.value = value;
                return;
            }
        }

        bucket.emplace_back(key, value);
        size++;

        if (static_cast<double>(size) / numBuckets > 0.7) {
            resize();
        }
    }

    V get(K key) const {
        int bucketIndex = getBucketIndex(key);
        const auto& bucket = buckets[bucketIndex];

        for (const auto& node : bucket) {
            if (node.key == key) {
                return node.value;
            }
        }

        throw std::out_of_range("Key not found");
    }

    void remove(K key) {
        int bucketIndex = getBucketIndex(key);
        auto& bucket = buckets[bucketIndex];

        for (auto it = bucket.begin(); it != bucket.end(); ++it) {
            if (it->key == key) {
                bucket.erase(it);
                size--;
                return;
            }
        }
    }

    int getSize() const {
        return size;
    }
};
```

## Advanced Data Structures

### Trie

A Trie, also called a prefix tree, is a tree-like data structure used to store and retrieve strings. It's particularly useful for tasks involving string prefixes, such as autocomplete and spell checking.

Key Operations:
- Insert: O(m), where m is the length of the string
- Search: O(m)
- Delete: O(m)

Example implementation (Trie in C++):

```cpp
#include <unordered_map>
#include <string>

class Trie {
private:
    struct TrieNode {
        std::unordered_map<char, TrieNode*> children;
        bool isEndOfWord;
        TrieNode() : isEndOfWord(false) {}
    };

    TrieNode* root;

public:
    Trie() : root(new TrieNode()) {}

    void insert(const std::string& word) {
        TrieNode* current = root;
        for (char ch : word) {
            if (current->children.find(ch) == current->children.end()) {
                current->children[ch] = new TrieNode();
            }
            current = current->children[ch];
        }
        current->isEndOfWord = true;
    }

    bool search(const std::string& word) const {
        TrieNode* node = searchPrefix(word);
        return node != nullptr && node->isEndOfWord;
    }

    bool startsWith(const std::string& prefix) const {
        return searchPrefix(prefix) != nullptr;
    }

private:
    TrieNode* searchPrefix(const std::string& prefix) const {
        TrieNode* current = root;
        for (char ch : prefix) {
            if (current->children.find(ch) == current->children.end()) {
                return nullptr;
            }
            current = current->children[ch];
        }
        return current;
    }
};
```

### Segment Tree

A Segment Tree is a tree data structure used for storing information about intervals, or segments. It allows for efficient query operations over an array or list, especially for range queries.

Key Operations:
- Build: O(n)
- Query: O(log n)
- Update: O(log n)

Example implementation (Segment Tree for range sum queries in C++):

```cpp
#include <vector>

class SegmentTree {
private:
    std::vector<int> tree;
    int n;

    void buildTree(const std::vector<int>& arr, int v, int tl, int tr) {
        if (tl == tr) {
            tree[v] = arr[tl];
        } else {
            int tm = (tl + tr) / 2;
            buildTree(arr, v * 2 + 1, tl, tm);
            buildTree(arr, v * 2 + 2, tm + 1, tr);
            tree[v] = tree[v * 2 + 1] + tree[v * 2 + 2];
        }
    }

    int queryRec(int v, int tl, int tr, int l, int r) const {
        if (l > r) return 0;
        if (l == tl && r == tr) return tree[v];
        int tm = (tl + tr) / 2;
        return queryRec(v * 2 + 1, tl, tm, l, std::min(r, tm))
             + queryRec(v * 2 + 2, tm + 1, tr, std::max(l, tm + 1), r);
    }

    void updateRec(int v, int tl, int tr, int pos, int newVal) {
        if (tl == tr) {
            tree[v] = newVal;
        } else {
            int tm = (tl + tr) / 2;
            if (pos <= tm) {
                updateRec(v * 2 + 1, tl, tm, pos, newVal);
            } else {
                updateRec(v * 2 + 2, tm + 1, tr, pos, newVal);
            }
            tree[v] = tree[v * 2 + 1] + tree[v * 2 + 2];
        }
    }

public:
    SegmentTree(const std::vector<int>& arr) : n(arr.size()) {
        tree.resize(4 * n);
        buildTree(arr, 0, 0, n - 1);
    }

    int query(int l, int r) const {
        return queryRec(0, 0, n - 1, l, r);
    }

    void update(int pos, int newVal) {
        updateRec(0, 0, n - 1, pos, newVal);
    }
};
```

### Fenwick Tree (Binary Indexed Tree)

A Fenwick Tree, also known as a Binary Indexed Tree, is a data structure that can efficiently update elements and calculate prefix sums in a table of numbers.

Key Operations:
- Update: O(log n)
- Query (Prefix Sum): O(log n)

Example implementation (Fenwick Tree in C++):

```cpp
#include <vector>

class FenwickTree {
private:
    std::vector<int> tree;

public:
    FenwickTree(int n) : tree(n + 1, 0) {}

    void update(int i, int delta) {
        while (i < tree.size()) {
            tree[i] += delta;
            i += i & (-i);
        }
    }

    int query(int i) const {
        int sum = 0;
        while (i > 0) {
            sum += tree[i];
            i -= i & (-i);
        }
        return sum;
    }

    int rangeQuery(int left, int right) const {
        return query(right) - query(left - 1);
    }
};
```

### Disjoint Set (Union-Find)

A Disjoint Set data structure, also known as Union-Find, keeps track of a set of elements partitioned into a number of disjoint (non-overlapping) subsets.

Key Operations:
- Find: O(α(n)), where α is the inverse Ackermann function
- Union: O(α(n))

Example implementation (Disjoint Set with path compression and union by rank in C++):

```cpp
#include <vector>

class DisjointSet {
private:
    std::vector<int> parent;
    std::vector<int> rank;

public:
    DisjointSet(int n) : parent(n), rank(n, 0) {
        for (int i = 0; i < n; i++) {
            parent[i] = i;
        }
    }

    int find(int x) {
        if (parent[x] != x) {
            parent[x] = find(parent[x]);
        }
        return parent[x];
    }

    void unionSets(int x, int y) {
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
};
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

We hope this comprehensive guide to data structures in C++ helps you in your journey to becoming a better programmer and computer scientist. Happy coding!