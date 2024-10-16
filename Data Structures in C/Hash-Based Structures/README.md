# Hash-Based Structures in C

## Table of Contents
- [Hash-Based Structures in C](#hash-based-structures-in-c)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Hash Functions](#hash-functions)
    - [Characteristics of Good Hash Functions:](#characteristics-of-good-hash-functions)
    - [Common Hash Functions:](#common-hash-functions)
  - [Hash Tables](#hash-tables)
    - [Components:](#components)
    - [Operations:](#operations)
  - [Collision Resolution](#collision-resolution)
    - [1. Chaining (Open Hashing):](#1-chaining-open-hashing)
    - [2. Open Addressing (Closed Hashing):](#2-open-addressing-closed-hashing)
  - [Load Factor and Resizing](#load-factor-and-resizing)
    - [Resizing:](#resizing)
    - [Time Complexity:](#time-complexity)
  - [Hash Sets](#hash-sets)
    - [Characteristics:](#characteristics)
    - [Operations:](#operations-1)
  - [Hash Maps](#hash-maps)
    - [Characteristics:](#characteristics-1)
    - [Operations:](#operations-2)
  - [Bloom Filters](#bloom-filters)
    - [Characteristics:](#characteristics-2)
    - [Operations:](#operations-3)
  - [Cuckoo Hashing](#cuckoo-hashing)
    - [Characteristics:](#characteristics-3)
    - [Operations:](#operations-4)
  - [Time Complexity](#time-complexity-1)
  - [Memory Management](#memory-management)
  - [Best Practices](#best-practices)
  - [Common Use Cases](#common-use-cases)
  - [Limitations and Considerations](#limitations-and-considerations)
  - [Examples](#examples)
  - [Further Resources](#further-resources)

## Introduction

Hash-based structures are fundamental data structures in computer science that use hash functions to map keys to array indices. These structures provide efficient insertion, deletion, and lookup operations, making them crucial for various applications in software development.

This README provides an in-depth overview of hash-based structures implemented in C, including their types, characteristics, operations, and best practices for implementation.

## Hash Functions

Hash functions are the core of hash-based structures. They convert keys into array indices.

### Characteristics of Good Hash Functions:
- Deterministic: Same input always produces the same output
- Uniform distribution: Spreads keys evenly across the array
- Efficiency: Computes quickly
- Avalanche effect: Small changes in input cause significant changes in output

### Common Hash Functions:
1. Division method
2. Multiplication method
3. Universal hashing
4. Cryptographic hash functions (e.g., SHA-256, MD5)

## Hash Tables

Hash tables are the most common hash-based structure, providing average-case O(1) time complexity for insertions, deletions, and lookups.

### Components:
1. Array of buckets
2. Hash function
3. Collision resolution method

### Operations:
- Insert
- Delete
- Search
- Resize

## Collision Resolution

Collisions occur when two keys hash to the same index. There are several methods to handle collisions:

### 1. Chaining (Open Hashing):
- Each bucket contains a linked list of elements
- Pros: Simple to implement, works well with high load factors
- Cons: Requires additional memory for pointers

### 2. Open Addressing (Closed Hashing):
- All elements are stored in the hash table itself
- Types:
  a. Linear Probing
  b. Quadratic Probing
  c. Double Hashing
- Pros: Better cache performance, no extra memory for pointers
- Cons: Risk of primary and secondary clustering, more sensitive to load factor

## Load Factor and Resizing

The load factor (α) is the ratio of occupied slots to the total slots in the hash table.

### Resizing:
- Typically done when α exceeds a threshold (e.g., 0.75)
- Process:
  1. Create a new array (usually double the size)
  2. Rehash all elements into the new array
  3. Replace the old array with the new one

### Time Complexity:
- Amortized O(1) for insertions with occasional O(n) resizing operations

## Hash Sets

Hash sets are collections that store unique elements using a hash table.

### Characteristics:
- No duplicate elements
- No particular order
- Efficient membership testing

### Operations:
- Add
- Remove
- Contains

## Hash Maps

Hash maps (also known as hash tables or dictionaries) store key-value pairs.

### Characteristics:
- Each key is unique
- Values can be duplicated
- Efficient key-based retrieval

### Operations:
- Put (key, value)
- Get (key)
- Remove (key)
- Contains Key

## Bloom Filters

Bloom filters are space-efficient probabilistic data structures used to test whether an element is a member of a set.

### Characteristics:
- Can have false positives, but no false negatives
- Very space-efficient for large sets
- Cannot remove elements (counting Bloom filters can support deletion)

### Operations:
- Add
- Test

## Cuckoo Hashing

Cuckoo hashing is a technique that uses two hash functions and guarantees O(1) worst-case lookup time.

### Characteristics:
- Uses two hash tables
- Each key can be in one of two possible positions
- Insertion may require moving existing keys

### Operations:
- Insert
- Delete
- Lookup

## Time Complexity

| Operation | Average Case | Worst Case |
|-----------|--------------|------------|
| Insertion | O(1)         | O(n)       |
| Deletion  | O(1)         | O(n)       |
| Search    | O(1)         | O(n)       |

Note: Worst-case scenarios are rare with a good hash function and appropriate resizing.

## Memory Management

Proper memory management is crucial when implementing hash-based structures in C:

1. Allocate memory for the hash table array dynamically.
2. Free memory for individual elements (if dynamically allocated) when removing them.
3. Free all allocated memory when destroying the hash table.
4. Use valgrind or similar tools to check for memory leaks.

## Best Practices

1. Choose an appropriate initial size for the hash table to minimize early resizing.
2. Implement a good hash function that distributes keys uniformly.
3. Use prime numbers for the table size to reduce collisions.
4. Implement proper error handling for memory allocation failures.
5. Use typedef to create aliases for struct types to improve code readability.
6. Implement separate functions for different operations (e.g., insert, delete, search).
7. Use const qualifiers for parameters that shouldn't be modified.
8. Document your code, especially the hash function and collision resolution method.

## Common Use Cases

1. Caching (e.g., memoization in dynamic programming)
2. Symbol tables in compilers and interpreters
3. Database indexing
4. Implementing sets and maps in various algorithms
5. Spell checkers
6. Counting distinct elements in a stream
7. Detecting duplicate items (e.g., in a large dataset)

## Limitations and Considerations

1. Hash tables are not suitable for operations that require ordered data.
2. The efficiency of hash tables depends heavily on the quality of the hash function.
3. Hash tables can have poor performance with a bad choice of initial size and growth strategy.
4. Open addressing schemes can suffer from primary and secondary clustering.
5. Cryptographic hash functions, while secure, are often too slow for general-purpose hash tables.

## Examples

Here are some example implementations of hash-based structures in C:

1. [Simple Hash Table with Chaining](https://github.com/example/c-hash-structures/hash_table_chaining.c)
2. [Hash Table with Open Addressing](https://github.com/example/c-hash-structures/hash_table_open_addressing.c)
3. [Hash Set Implementation](https://github.com/example/c-hash-structures/hash_set.c)
4. [Hash Map Implementation](https://github.com/example/c-hash-structures/hash_map.c)
5. [Bloom Filter](https://github.com/example/c-hash-structures/bloom_filter.c)

## Further Resources

1. "Introduction to Algorithms" by Thomas H. Cormen, Charles E. Leiserson, Ronald L. Rivest, and Clifford Stein
2. "The Art of Computer Programming, Volume 3: Sorting and Searching" by Donald E. Knuth
3. "Algorithms in C, Parts 1-4: Fundamentals, Data Structures, Sorting, Searching" by Robert Sedgewick
4. [MIT OpenCourseWare - Advanced Data Structures](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-851-advanced-data-structures-spring-2012/)
5. [Stanford CS166 - Data Structures](http://web.stanford.edu/class/cs166/)
6. [GeeksforGeeks - Hashing Data Structure](https://www.geeksforgeeks.org/hashing-data-structure/)

Remember to practice implementing these hash-based structures and solve problems using them to gain a deeper understanding of their applications and efficiency. Each structure has its own strengths and weaknesses, and choosing the right one can significantly impact the performance of your programs.