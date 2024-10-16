# Linear Data Structures in C

## Table of Contents
1. [Introduction](#introduction)
2. [Arrays](#arrays)
3. [Linked Lists](#linked-lists)
4. [Stacks](#stacks)
5. [Queues](#queues)
6. [Deques](#deques)
7. [Strings](#strings)
8. [Vectors](#vectors)
9. [Time Complexity](#time-complexity)
10. [Memory Management](#memory-management)
11. [Best Practices](#best-practices)
12. [Further Resources](#further-resources)

## Introduction

Linear data structures are fundamental components in computer science and programming. They are collections of data elements arranged in a linear sequence. In C programming, understanding and implementing these structures is crucial for efficient data management and algorithm design.

This README provides an overview of all possible linear data structures in C. Each section includes definitions, characteristics, and operations.

## Arrays

Arrays are the simplest and most widely used linear data structure. They store elements of the same data type in contiguous memory locations.

### Characteristics:
- Fixed size (in C)
- Random access (constant time)
- Efficient for searching if sorted

### Basic Operations:
- Insertion: O(n) for unsorted, O(1) for end insertion
- Deletion: O(n)
- Search: O(n) for unsorted, O(log n) for sorted (using binary search)
- Access: O(1)

### Types:
1. One-dimensional arrays
2. Multi-dimensional arrays

## Linked Lists

Linked lists consist of nodes, where each node contains data and a reference (or link) to the next node in the sequence.

### Types:
1. Singly Linked List
2. Doubly Linked List
3. Circular Linked List
4. Circular Doubly Linked List

### Characteristics:
- Dynamic size
- Efficient insertion and deletion
- Sequential access

### Basic Operations:
- Insertion: O(1) if position is known, O(n) otherwise
- Deletion: O(1) if position is known, O(n) otherwise
- Search: O(n)
- Access: O(n)

## Stacks

Stacks are Last-In-First-Out (LIFO) data structures, where elements are added and removed from the same end.

### Characteristics:
- LIFO principle
- Can be implemented using arrays or linked lists

### Basic Operations:
- Push: O(1)
- Pop: O(1)
- Peek/Top: O(1)

## Queues

Queues are First-In-First-Out (FIFO) data structures, where elements are added at one end and removed from the other.

### Types:
1. Simple Queue
2. Circular Queue
3. Priority Queue
4. Double-ended Queue (Deque)

### Characteristics:
- FIFO principle
- Can be implemented using arrays or linked lists

### Basic Operations:
- Enqueue: O(1)
- Dequeue: O(1)
- Front: O(1)
- Rear: O(1)

## Deques

Deques (Double-ended queues) are a special type of queue where insertion and deletion can be performed at both ends.

### Characteristics:
- Elements can be added or removed from either end
- Can be implemented using arrays or linked lists

### Basic Operations:
- InsertFront: O(1)
- InsertRear: O(1)
- DeleteFront: O(1)
- DeleteRear: O(1)
- GetFront: O(1)
- GetRear: O(1)

## Strings

Strings are sequences of characters and can be considered a linear data structure in C.

### Characteristics:
- Null-terminated character arrays in C
- Immutable (modifications create new strings)

### Basic Operations:
- Length calculation: O(n)
- Concatenation: O(n+m) where n and m are lengths of strings
- Substring search: O(nm) using naive approach, O(n+m) using KMP algorithm

## Vectors

Vectors are dynamic arrays that can grow or shrink in size. While not natively supported in C, they can be implemented using dynamic memory allocation.

### Characteristics:
- Dynamic size
- Random access
- Efficient for adding/removing elements at the end

### Basic Operations:
- Insertion at end: O(1) amortized
- Deletion at end: O(1)
- Insertion/Deletion at arbitrary position: O(n)
- Access: O(1)

## Time Complexity

Understanding the time complexity of operations on these data structures is crucial for efficient algorithm design. Here's a summary:

| Operation | Array | Linked List | Stack | Queue | Deque |
|-----------|-------|-------------|-------|-------|-------|
| Access    | O(1)  | O(n)        | O(1)  | O(1)  | O(1)  |
| Search    | O(n)  | O(n)        | O(n)  | O(n)  | O(n)  |
| Insertion | O(n)  | O(1)        | O(1)  | O(1)  | O(1)  |
| Deletion  | O(n)  | O(1)        | O(1)  | O(1)  | O(1)  |

## Memory Management

Proper memory management is crucial when working with dynamic data structures in C:

1. Always free allocated memory to prevent memory leaks.
2. Use valgrind or similar tools to check for memory leaks.
3. Be cautious of dangling pointers after freeing memory.
4. Initialize pointers to NULL when declaring.

## Best Practices

1. Choose the appropriate data structure based on the problem requirements.
2. Always check for NULL when working with pointers.
3. Implement error handling for operations like push on a full stack or dequeue from an empty queue.
4. Use typedef to create aliases for struct types to improve code readability.
5. Implement helper functions for common operations (e.g., createNode, freeList).
6. Use const qualifiers for parameters that shouldn't be modified.
7. Follow consistent naming conventions for functions and variables.
8. Comment your code, especially for complex operations or algorithms.

## Further Resources

1. "Data Structures and Algorithms in C" by Michael T. Goodrich
2. "The C Programming Language" by Brian W. Kernighan and Dennis M. Ritchie
3. "Advanced Data Structures" by Peter Brass
4. "Introduction to Algorithms" by Thomas H. Cormen, Charles E. Leiserson, Ronald L. Rivest, and Clifford Stein
5. [GeeksforGeeks - Data Structures](https://www.geeksforgeeks.org/data-structures/)
6. [Coursera - Data Structures and Algorithms Specialization](https://www.coursera.org/specializations/data-structures-algorithms)
7. [MIT OpenCourseWare - Introduction to Algorithms](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-006-introduction-to-algorithms-fall-2011/)

Remember to practice implementing these data structures and solving problems using them to gain a deeper understanding of their applications and efficiency. Each data structure has its own strengths and weaknesses, and choosing the right one can significantly impact the performance of your programs.