# DATA STRUCTURES & ALGORITHMS

## Chapter 1: Introduction to DSA

* What are Data Structures and Algorithms?
* Why DSA matters in software development and interviews
* Algorithm efficiency: Time and Space complexity
* Asymptotic notations: Big-O, Big-Omega, Big-Theta
* Common complexity classes: O(1), O(log n), O(n), O(n log n), O(n²), O(2ⁿ), O(n!)

---

## Chapter 2: Mathematics & Prerequisites

* Recursion basics: Base case, recursive case, call stack
* Backtracking principles
* Mathematical foundations:

  * Logarithms and exponents
  * Summations and series
  * Permutations and combinations
  * Modular arithmetic
  * Prime numbers and GCD

* Bit manipulation:

  * Bitwise operators (AND, OR, XOR, NOT, shifts)
  * Common tricks: checking power of two, toggling bits, counting set bits

---

## Chapter 3: Arrays and Strings

### Arrays

* One-dimensional and multi-dimensional arrays
* Dynamic arrays (e.g., ArrayList, Vector)
* Common operations: traversal, insertion, deletion, searching
* Prefix sum array
* Difference array

### Sliding Window Technique

* Fixed-size window
* Variable-size window

### Two Pointers Technique

* Opposite direction (pair sum, palindrome)
* Same direction (remove duplicates, merge sorted arrays)

### Strings

* String immutability and builders
* Pattern matching algorithms:

  * Naive search
  * KMP (Knuth-Morris-Pratt)
  * Rabin-Karp (rolling hash)

* Anagram and palindrome problems

### Important Problems

* Kadane’s Algorithm (maximum subarray sum)
* Dutch National Flag problem (sort 0,1,2)
* Trapping rainwater
* Container with most water

---

## Chapter 4: Linked Lists

* Singly Linked List
* Doubly Linked List
* Circular Linked List
* Basic operations: insertion, deletion, traversal, search
* Two-pointer techniques:

  * Finding middle of list
  * Cycle detection (Floyd’s cycle detection)
  * Finding start of cycle

* Reversal:

  * Iterative reversal
  * Recursive reversal
  * Reverse in groups of k

* Merge and intersection problems:

  * Merge two sorted lists
  * Find intersection point of two lists

* Copy list with random pointer

---

## Chapter 5: Stacks and Queues

### Stack

* LIFO principle
* Array-based implementation
* Linked-list-based implementation
* Applications:

  * Balanced parentheses
  * Expression evaluation (infix, postfix, prefix)
  * Next Greater Element
  * Largest rectangle in histogram
  * Min stack (supporting getMin in O(1))

### Queue

* FIFO principle
* Array-based (circular queue) and linked-list implementations
* Double-ended queue (Deque)
* Applications:

  * Sliding window maximum
  * BFS traversal

### Priority Queue (Heap)

* Min-heap and max-heap
* Heapify and heap operations (insert, extract min/max, decrease key)
* Applications:

  * Kth largest/smallest element
  * Merge K sorted lists
  * Dijkstra’s algorithm support

---

## Chapter 6: Recursion and Backtracking

* Recursion fundamentals: base case, recurrence relation
* Tail recursion vs non-tail recursion
* Recursion vs iteration

### Backtracking

* State space tree
* Pruning techniques
* Classic problems:

  * N-Queens
  * Sudoku solver
  * Rat in a maze
  * Generate all subsets (powerset)
  * Generate permutations
  * Combination sum

---

## Chapter 7: Sorting and Searching

### Sorting Algorithms

| Algorithm     | Best Case | Average Case | Worst Case | Space | Stable |
|---------------|-----------|--------------|------------|-------|--------|
| Bubble Sort   | O(n)      | O(n²)        | O(n²)      | O(1)  | Yes    |
| Selection Sort| O(n²)     | O(n²)        | O(n²)      | O(1)  | No     |
| Insertion Sort| O(n)      | O(n²)        | O(n²)      | O(1)  | Yes    |
| Merge Sort    | O(n log n)| O(n log n)   | O(n log n) | O(n)  | Yes    |
| Quick Sort    | O(n log n)| O(n log n)   | O(n²)      | O(log n)| No  |
| Heap Sort     | O(n log n)| O(n log n)   | O(n log n) | O(1)  | No     |
| Counting Sort | O(n+k)    | O(n+k)       | O(n+k)     | O(k)  | Yes    |
| Radix Sort    | O(nk)     | O(nk)        | O(nk)      | O(n+k)| Yes    |

* Comparison-based vs non-comparison sorts
* In-place vs out-of-place
* Adaptive sorts

### Searching

* Linear search
* Binary search (iterative and recursive)
* Variations:

  * First/last occurrence
  * Search in rotated sorted array
  * Find peak element

* Ternary search

---

## Chapter 8: Hashing

* Hash functions
* Collision resolution:

  * Chaining (linked lists)
  * Open addressing (linear probing, quadratic probing, double hashing)

* Load factor and rehashing
* Hash map and hash set implementations
* Applications:

  * Two-sum problem
  * Subarray sum equals K
  * Longest consecutive sequence
  * Group anagrams
  * LRU Cache (using hash map + doubly linked list)

---

## Chapter 9: Trees

### Binary Trees

* Tree terminology: root, parent, child, leaf, height, depth
* Binary tree traversals (DFS and BFS):

  * Inorder, Preorder, Postorder (recursive and iterative)
  * Level order traversal

* Construction of tree from traversals
* Diameter of binary tree
* Lowest Common Ancestor (LCA)
* Maximum path sum

### Binary Search Trees (BST)

* Properties: left < root < right
* Search, insert, delete (successor/predecessor)
* Validate BST
* Kth smallest/largest element
* Range sum queries

### Balanced BSTs (conceptual)

* AVL trees (rotations, balance factor)
* Red-Black trees (rules, use cases)

### Heap (Binary Heap)

* Array representation
* Min-heap and max-heap operations
* Heap sort
* Priority queue implementation

### Advanced Trees

* Trie (prefix tree) – insertion, search, deletion, auto-complete
* Segment tree (range queries, point updates, lazy propagation)
* Fenwick tree (Binary Indexed Tree)
* Disjoint Set Union (Union-Find) – path compression, union by rank

---

## Chapter 10: Graphs

### Graph Representations

* Adjacency matrix
* Adjacency list
* Edge list

### Graph Traversals

* Depth First Search (DFS) – recursive and iterative
* Breadth First Search (BFS)

### Shortest Path Algorithms

* Unweighted graph: BFS
* Weighted graph (non-negative): Dijkstra’s algorithm (using min-heap)
* Weighted graph (negative edges): Bellman-Ford algorithm
* All-pairs shortest paths: Floyd-Warshall algorithm

### Minimum Spanning Tree (MST)

* Prim’s algorithm
* Kruskal’s algorithm (using Union-Find)

### Topological Sorting

* Kahn’s algorithm (BFS-based)
* DFS-based

### Cycle Detection

* Undirected graph (using DFS or Union-Find)
* Directed graph (using DFS recursion stack or colors)

### Strongly Connected Components

* Kosaraju’s algorithm
* Tarjan’s algorithm

### Network Flow (basic)

* Max flow / min cut (Ford-Fulkerson, Edmonds-Karp)

### Important Graph Problems

* Clone a graph
* Word ladder (BFS)
* Course schedule (topological sort)
* Number of islands (DFS/BFS)
* Bipartite graph checking

---

## Chapter 11: Dynamic Programming (DP)

### DP Fundamentals

* Overlapping subproblems
* Optimal substructure
* Memoization (top-down) vs Tabulation (bottom-up)

### Classic DP Problems

* Fibonacci numbers
* Climbing stairs
* House robber (1D DP)
* Minimum path sum (grid)
* Unique paths (grid)

### Subsequence and Substring Problems

* Longest Common Subsequence (LCS)
* Longest Common Substring
* Longest Increasing Subsequence (LIS)
* Edit distance (Levenshtein distance)

### Subset and Knapsack Problems

* 0/1 Knapsack
* Subset sum
* Partition equal subset sum

### DP on Strings

* Palindrome partitioning
* Wildcard matching
* Regular expression matching

### DP on Trees

* Tree DP (maximum independent set, tree diameter)

### DP with Bitmask

* Travelling Salesman Problem (TSP)

### Kadane’s Algorithm (maximum subarray sum – DP view)

---

## Chapter 12: Greedy Algorithms

* Greedy choice property
* Activity selection
* Fractional knapsack
* Job sequencing with deadlines
* Huffman coding
* Coin change (greedy vs DP)
* Minimum number of platforms (interval scheduling)

---

## Chapter 13: Important Interview Topics

* Array vs Linked List
* Stack vs Queue vs Heap
* Recursion vs Iteration
* DFS vs BFS
* Hash Map vs Tree Map
* Comparison of sorting algorithms (stability, in-place, time/space)
* Singly vs Doubly Linked List
* Binary Search Tree vs Hash Table
* When to use DP vs Greedy vs Backtracking
* Union-Find applications
* Trie vs Hash Table for string search
* Two-pointer vs Sliding Window

---

## Chapter 14: Complexity Analysis & Numerical Problems

* Recurrence relations and Master Theorem
* Amortized analysis (dynamic arrays, increment counters)
* Space-time trade-offs

### Numerical Problems

* Power of a number (fast exponentiation)
* Sieve of Eratosthenes (prime generation)
* Greatest Common Divisor (Euclidean algorithm)
* Modular exponentiation
* Factorial of large numbers (handling overflow)
* Catalan numbers

---

## Chapter 15: Advanced & Miscellaneous Topics

* Monotonic stack (next greater element, largest rectangle)
* Deque applications (sliding window maximum)
* Multiset and ordered set (Balanced BST in libraries)
* Rolling hash (Rabin-Karp)
* Boyer-Moore majority vote algorithm
* Moore’s voting algorithm for majority element
* Reservoir sampling (random sampling from stream)
* Interval merging and partitioning
* Meeting rooms II (min meeting rooms required)
* Randomized algorithms (quickselect, randomized quicksort)

---

## Support

If this repository adds value to your learning, consider giving it a star to show your support. Contributions, corrections, and additional problem lists are welcome.