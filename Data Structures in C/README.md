# 🌟 Data Structures Compendium in C 🌟

Welcome to the comprehensive guide to Data Structures implemented in C! This repository serves as an extensive resource for understanding, implementing, and mastering various data structures crucial to computer science and software engineering.

## 📚 Table of Contents

- [🌟 Data Structures Compendium in C 🌟](#-data-structures-compendium-in-c-)
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
2. Dynamic Arrays: Resizable arrays (implemented using pointers and memory allocation in C)

Key Operations:
- Access: O(1)
- Search: O(n) for unsorted, O(log n) for sorted (using binary search)
- Insertion: O(n) (worst case, when inserting at the beginning)
- Deletion: O(n) (worst case, when deleting from the beginning)

Example implementation (Dynamic Array in C):

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    int* array;
    int size;
    int capacity;
} DynamicArray;

DynamicArray* createDynamicArray() {
    DynamicArray* arr = (DynamicArray*)malloc(sizeof(DynamicArray));
    arr->array = (int*)malloc(sizeof(int));
    arr->size = 0;
    arr->capacity = 1;
    return arr;
}

void add(DynamicArray* arr, int element) {
    if (arr->size == arr->capacity) {
        arr->capacity *= 2;
        arr->array = (int*)realloc(arr->array, arr->capacity * sizeof(int));
    }
    arr->array[arr->size++] = element;
}

int get(DynamicArray* arr, int index) {
    if (index < 0 || index >= arr->size) {
        printf("Index out of bounds\n");
        exit(1);
    }
    return arr->array[index];
}

void freeDynamicArray(DynamicArray* arr) {
    free(arr->array);
    free(arr);
}
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

Example implementation (Singly Linked List in C):

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Node {
    int data;
    struct Node* next;
} Node;

typedef struct {
    Node* head;
} LinkedList;

LinkedList* createLinkedList() {
    LinkedList* list = (LinkedList*)malloc(sizeof(LinkedList));
    list->head = NULL;
    return list;
}

void append(LinkedList* list, int data) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->data = data;
    newNode->next = NULL;

    if (list->head == NULL) {
        list->head = newNode;
        return;
    }

    Node* current = list->head;
    while (current->next != NULL) {
        current = current->next;
    }
    current->next = newNode;
}

void delete(LinkedList* list, int data) {
    if (list->head == NULL) return;

    if (list->head->data == data) {
        Node* temp = list->head;
        list->head = list->head->next;
        free(temp);
        return;
    }

    Node* current = list->head;
    while (current->next != NULL && current->next->data != data) {
        current = current->next;
    }

    if (current->next != NULL) {
        Node* temp = current->next;
        current->next = current->next->next;
        free(temp);
    }
}

void freeLinkedList(LinkedList* list) {
    Node* current = list->head;
    while (current != NULL) {
        Node* temp = current;
        current = current->next;
        free(temp);
    }
    free(list);
}
```

### Stacks

Stacks follow the Last-In-First-Out (LIFO) principle. The last element added to the stack will be the first one to be removed.

Key Operations:
- Push: O(1)
- Pop: O(1)
- Peek (Top): O(1)

Example implementation (Stack using C array):

```c
#include <stdio.h>
#include <stdlib.h>

#define MAX_SIZE 100

typedef struct {
    int items[MAX_SIZE];
    int top;
} Stack;

Stack* createStack() {
    Stack* stack = (Stack*)malloc(sizeof(Stack));
    stack->top = -1;
    return stack;
}

int isEmpty(Stack* stack) {
    return stack->top == -1;
}

void push(Stack* stack, int item) {
    if (stack->top == MAX_SIZE - 1) {
        printf("Stack Overflow\n");
        return;
    }
    stack->items[++stack->top] = item;
}

int pop(Stack* stack) {
    if (isEmpty(stack)) {
        printf("Stack Underflow\n");
        exit(1);
    }
    return stack->items[stack->top--];
}

int peek(Stack* stack) {
    if (isEmpty(stack)) {
        printf("Stack is empty\n");
        exit(1);
    }
    return stack->items[stack->top];
}

void freeStack(Stack* stack) {
    free(stack);
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

Example implementation (Queue using C array):

```c
#include <stdio.h>
#include <stdlib.h>

#define MAX_SIZE 100

typedef struct {
    int items[MAX_SIZE];
    int front;
    int rear;
} Queue;

Queue* createQueue() {
    Queue* queue = (Queue*)malloc(sizeof(Queue));
    queue->front = -1;
    queue->rear = -1;
    return queue;
}

int isEmpty(Queue* queue) {
    return queue->front == -1;
}

void enqueue(Queue* queue, int item) {
    if (queue->rear == MAX_SIZE - 1) {
        printf("Queue Overflow\n");
        return;
    }
    if (isEmpty(queue)) {
        queue->front = 0;
    }
    queue->items[++queue->rear] = item;
}

int dequeue(Queue* queue) {
    if (isEmpty(queue)) {
        printf("Queue Underflow\n");
        exit(1);
    }
    int item = queue->items[queue->front];
    if (queue->front == queue->rear) {
        queue->front = -1;
        queue->rear = -1;
    } else {
        queue->front++;
    }
    return item;
}

int front(Queue* queue) {
    if (isEmpty(queue)) {
        printf("Queue is empty\n");
        exit(1);
    }
    return queue->items[queue->front];
}

int rear(Queue* queue) {
    if (isEmpty(queue)) {
        printf("Queue is empty\n");
        exit(1);
    }
    return queue->items[queue->rear];
}

void freeQueue(Queue* queue) {
    free(queue);
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

Example implementation (Binary Search Tree in C):

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Node {
    int value;
    struct Node* left;
    struct Node* right;
} Node;

Node* createNode(int value) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->value = value;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

Node* insert(Node* root, int value) {
    if (root == NULL) {
        return createNode(value);
    }

    if (value < root->value) {
        root->left = insert(root->left, value);
    } else if (value > root->value) {
        root->right = insert(root->right, value);
    }

    return root;
}

int search(Node* root, int value) {
    if (root == NULL || root->value == value) {
        return root != NULL;
    }

    if (value < root->value) {
        return search(root->left, value);
    }

    return search(root->right, value);
}

void freeTree(Node* root) {
    if (root != NULL) {
        freeTree(root->left);
        freeTree(root->right);
        free(root);
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

Example implementation (Graph using Adjacency List in C):

```c
#include <stdio.h>
#include <stdlib.h>

#define MAX_VERTICES 100

typedef struct Node {
    int vertex;
    struct Node* next;
} Node;

typedef struct {
    Node* head[MAX_VERTICES];
    int numVertices;
} Graph;

Graph* createGraph(int numVertices) {
    Graph* graph = (Graph*)malloc(sizeof(Graph));
    graph->numVertices = numVertices;

    for (int i = 0; i < numVertices; i++) {
        graph->head[i] = NULL;
    }

    return graph;
}

void addEdge(Graph* graph, int src, int dest) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->vertex = dest;
    newNode->next = graph->head[src];
    graph->head[src] = newNode;

    // For undirected graph, add an edge from dest to src as well
    newNode = (Node*)malloc(sizeof(Node));
    newNode->vertex = src;
    newNode->next = graph->head[dest];
    graph->head[dest] = newNode;
}

void DFS(Graph* graph, int vertex, int visited[]) {
    visited[vertex] = 1;
    printf("%d ", vertex);

    Node* temp = graph->head[vertex];
    while (temp != NULL) {
        if (!visited[temp->vertex]) {
            DFS(graph, temp->vertex, visited);
        }
        temp = temp->next;
    }
}

void freeGraph(Graph* graph) {
    for (int i = 0; i < graph->numVertices; i++) {
        Node* temp = graph->head[i];
        while (temp != NULL) {
            Node* next = temp->next;
            free(temp);
            temp = next;
        }
    }
    free(graph);
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

Example implementation (Binary Max Heap in C):

```c
#include <stdio.h>
#include <stdlib.h>

#define MAX_SIZE 100

typedef struct {
    int* heap;
    int size;
    int capacity;
} MaxHeap;

MaxHeap* createMaxHeap(int capacity) {
    MaxHeap* maxHeap = (MaxHeap*)malloc(sizeof(MaxHeap));
    maxHeap->heap = (int*)malloc(capacity * sizeof(int));
    maxHeap->size = 0;
    maxHeap->capacity = capacity;
    return maxHeap;
}

void swap(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

void heapifyUp(MaxHeap* maxHeap, int index) {
    int parent = (index - 1) / 2;
    if (index > 0 && maxHeap->heap[index] > maxHeap->heap[parent]) {
        swap(&maxHeap->heap[index], &maxHeap->heap[parent]);
        heapifyUp(maxHeap, parent);
    }
}

void heapifyDown(MaxHeap* maxHeap, int index) {
    int largest = index;
    int left = 2 * index + 1;
    int right = 2 * index + 2;

    if (left < maxHeap->size && maxHeap->heap[left] > maxHeap->heap[largest]) {
        largest = left;
    }

    if (right < maxHeap->size && maxHeap->heap[right] > maxHeap->heap[largest]) {
        largest = right;
    }

    if (largest != index) {
        swap(&maxHeap->heap[index], &maxHeap->heap[largest]);
        heapifyDown(maxHeap, largest);
    }
}

void insert(MaxHeap* maxHeap, int key) {
    if (maxHeap->size == maxHeap->capacity) {
        printf("Heap is full\n");
        return;
    }

    maxHeap->size++;
    int index = maxHeap->size - 1;
    maxHeap->heap[index] = key;

    heapifyUp(maxHeap, index);
}

int extractMax(MaxHeap* maxHeap) {
    if (maxHeap->size <= 0) {
        printf("Heap is empty\n");
        return -1;
    }

    if (maxHeap->size == 1) {
        maxHeap->size--;
        return maxHeap->heap[0];
    }

    int root = maxHeap->heap[0];
    maxHeap->heap[0] = maxHeap->heap[maxHeap->size - 1];
    maxHeap->size--;
    heapifyDown(maxHeap, 0);

    return root;
}

void freeMaxHeap(MaxHeap* maxHeap) {
    free(maxHeap->heap);
    free(maxHeap);
}
```

## Hash-Based Structures

### Hash Tables

Hash tables are data structures that implement an associative array abstract data type, a structure that can map keys to values. They use a hash function to compute an index into an array of buckets or slots, from which the desired value can be found.

Key Operations:
- Insert: O(1) average, O(n) worst
- Delete: O(1) average, O(n) worst
- Search: O(1) average, O(n) worst

Example implementation (Hash Table with chaining in C):

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define TABLE_SIZE 100

typedef struct Node {
    char* key;
    int value;
    struct Node* next;
} Node;

typedef struct {
    Node* buckets[TABLE_SIZE];
} HashTable;

HashTable* createHashTable() {
    HashTable* hashTable = (HashTable*)malloc(sizeof(HashTable));
    for (int i = 0; i < TABLE_SIZE; i++) {
        hashTable->buckets[i] = NULL;
    }
    return hashTable;
}

unsigned int hash(char* key) {
    unsigned int hashValue = 0;
    for (int i = 0; key[i] != '\0'; i++) {
        hashValue = 31 * hashValue + key[i];
    }
    return hashValue % TABLE_SIZE;
}

void insert(HashTable* hashTable, char* key, int value) {
    unsigned int index = hash(key);
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->key = strdup(key);
    newNode->value = value;
    newNode->next = hashTable->buckets[index];
    hashTable->buckets[index] = newNode;
}

int get(HashTable* hashTable, char* key) {
    unsigned int index = hash(key);
    Node* current = hashTable->buckets[index];
    while (current != NULL) {
        if (strcmp(current->key, key) == 0) {
            return current->value;
        }
        current = current->next;
    }
    return -1; // Key not found
}

void freeHashTable(HashTable* hashTable) {
    for (int i = 0; i < TABLE_SIZE; i++) {
        Node* current = hashTable->buckets[i];
        while (current != NULL) {
            Node* temp = current;
            current = current->next;
            free(temp->key);
            free(temp);
        }
    }
    free(hashTable);
}
```

## Advanced Data Structures

### Trie

A Trie, also called a prefix tree, is a tree-like data structure used to store and retrieve strings. It's particularly useful for tasks involving string prefixes, such as autocomplete and spell checking.

Key Operations:
- Insert: O(m), where m is the length of the string
- Search: O(m)
- Delete: O(m)

Example implementation (Trie in C):

```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#include <string.h>

#define ALPHABET_SIZE 26

typedef struct TrieNode {
    struct TrieNode* children[ALPHABET_SIZE];
    bool isEndOfWord;
} TrieNode;

TrieNode* createNode() {
    TrieNode* node = (TrieNode*)malloc(sizeof(TrieNode));
    for (int i = 0; i < ALPHABET_SIZE; i++) {
        node->children[i] = NULL;
    }
    node->isEndOfWord = false;
    return node;
}

void insert(TrieNode* root, const char* key) {
    TrieNode* current = root;
    int length = strlen(key);

    for (int i = 0; i < length; i++) {
        int index = key[i] - 'a';
        if (!current->children[index]) {
            current->children[index] = createNode();
        }
        current = current->children[index];
    }

    current->isEndOfWord = true;
}

bool search(TrieNode* root, const char* key) {
    TrieNode* current = root;
    int length = strlen(key);

    for (int i = 0; i < length; i++) {
        int index = key[i] - 'a';
        if (!current->children[index]) {
            return false;
        }
        current = current->children[index];
    }

    return current->isEndOfWord;
}

void freeTrie(TrieNode* node) {
    if (node == NULL) {
        return;
    }

    for (int i = 0; i < ALPHABET_SIZE; i++) {
        freeTrie(node->children[i]);
    }

    free(node);
}
```

### Segment Tree

A Segment Tree is a tree data structure used for storing information about intervals, or segments. It allows for efficient query operations over an array or list, especially for range queries.

Key Operations:
- Build: O(n)
- Query: O(log n)
- Update: O(log n)

Example implementation (Segment Tree for range sum queries in C):

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    int* tree;
    int n;
} SegmentTree;

SegmentTree* createSegmentTree(int arr[], int n) {
    SegmentTree* segTree = (SegmentTree*)malloc(sizeof(SegmentTree));
    segTree->n = n;
    segTree->tree = (int*)malloc(4 * n * sizeof(int));
    buildTree(segTree, arr, 0, 0, n - 1);
    return segTree;
}

void buildTree(SegmentTree* segTree, int arr[], int v, int tl, int tr) {
    if (tl == tr) {
        segTree->tree[v] = arr[tl];
    } else {
        int tm = (tl + tr) / 2;
        buildTree(segTree, arr, v * 2 + 1, tl, tm);
        buildTree(segTree, arr, v * 2 + 2, tm + 1, tr);
        segTree->tree[v] = segTree->tree[v * 2 + 1] + segTree->tree[v * 2 + 2];
    }
}

int query(SegmentTree* segTree, int v, int tl, int tr, int l, int r) {
    if (l > r) {
        return 0;
    }
    if (l == tl && r == tr) {
        return segTree->tree[v];
    }
    int tm = (tl + tr) / 2;
    return query(segTree, v * 2 + 1, tl, tm, l, (r < tm ? r : tm))
         + query(segTree, v * 2 + 2, tm + 1, tr, (l > tm + 1 ? l : tm + 1), r);
}

void update(SegmentTree* segTree, int v, int tl, int tr, int pos, int newVal) {
    if (tl == tr) {
        segTree->tree[v] = newVal;
    } else {
        int tm = (tl + tr) / 2;
        if (pos <= tm) {
            update(segTree, v * 2 + 1, tl, tm, pos, newVal);
        } else {
            update(segTree, v * 2 + 2, tm + 1, tr, pos, newVal);
        }
        segTree->tree[v] = segTree->tree[v * 2 + 1] + segTree->tree[v * 2 + 2];
    }
}

void freeSegmentTree(SegmentTree* segTree) {
    free(segTree->tree);
    free(segTree);
}
```

### Fenwick Tree (Binary Indexed Tree)

A Fenwick Tree, also known as a Binary Indexed Tree, is a data structure that can efficiently update elements and calculate prefix sums in a table of numbers.

Key Operations:
- Update: O(log n)
- Query (Prefix Sum): O(log n)

Example implementation (Fenwick Tree in C):

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    int* tree;
    int size;
} FenwickTree;

FenwickTree* createFenwickTree(int n) {
    FenwickTree* ft = (FenwickTree*)malloc(sizeof(FenwickTree));
    ft->size = n + 1;
    ft->tree = (int*)calloc(ft->size, sizeof(int));
    return ft;
}

void update(FenwickTree* ft, int i, int delta) {
    while (i < ft->size) {
        ft->tree[i] += delta;
        i += i & (-i);
    }
}

int query(FenwickTree* ft, int i) {
    int sum = 0;
    while (i > 0) {
        sum += ft->tree[i];
        i -= i & (-i);
    }
    return sum;
}

int rangeQuery(FenwickTree* ft, int left, int right) {
    return query(ft, right) - query(ft, left - 1);
}

void freeFenwickTree(FenwickTree* ft) {
    free(ft->tree);
    free(ft);
}
```

### Disjoint Set (Union-Find)

A Disjoint Set data structure, also known as Union-Find, keeps track of a set of elements partitioned into a number of disjoint (non-overlapping) subsets.

Key Operations:
- Find: O(α(n)), where α is the inverse Ackermann function
- Union: O(α(n))

Example implementation (Disjoint Set with path compression and union by rank in C):

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    int* parent;
    int* rank;
    int size;
} DisjointSet;

DisjointSet* createDisjointSet(int n) {
    DisjointSet* ds = (DisjointSet*)malloc(sizeof(DisjointSet));
    ds->size = n;
    ds->parent = (int*)malloc(n * sizeof(int));
    ds->rank = (int*)calloc(n, sizeof(int));

    for (int i = 0; i < n; i++) {
        ds->parent[i] = i;
    }

    return ds;
}

int find(DisjointSet* ds, int x) {
    if (ds->parent[x] != x) {
        ds->parent[x] = find(ds, ds->parent[x]);
    }
    return ds->parent[x];
}

void unionSets(DisjointSet* ds, int x, int y) {
    int rootX = find(ds, x);
    int rootY = find(ds, y);

    if (rootX != rootY) {
        if (ds->rank[rootX] < ds->rank[rootY]) {
            ds->parent[rootX] = rootY;
        } else if (ds->rank[rootX] > ds->rank[rootY]) {
            ds->parent[rootY] = rootX;
        } else {
            ds->parent[rootY] = rootX;
            ds->rank[rootX]++;
        }
    }
}

void freeDisjointSet(DisjointSet* ds) {
    free(ds->parent);
    free(ds->rank);
    free(ds);
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

We hope this comprehensive guide to data structures in C helps you in your journey to becoming a better programmer and computer scientist. Happy coding!
