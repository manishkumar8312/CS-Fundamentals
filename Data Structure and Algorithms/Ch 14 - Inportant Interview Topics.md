# Chapter 14: Important Interview Topics

This chapter synthesises key comparisons between data structures, algorithms, and problem‑solving paradigms that frequently appear in technical interviews. Each section highlights trade‑offs, use cases, and typical interview questions.

## 1. Array vs Linked List

| Feature | Array | Linked List |
|---------|-------|--------------|
| Memory | Contiguous block | Non‑contiguous, nodes linked by pointers |
| Access by index | O(1) | O(n) (traversal required) |
| Insertion/Deletion at beginning | O(n) (shift elements) | O(1) (update head pointer) |
| Insertion/Deletion at end (if tail known) | Amortized O(1) for dynamic array | O(1) with tail pointer |
| Insertion/Deletion at arbitrary position | O(n) | O(n) to find position, O(1) to update pointers |
| Memory overhead | Minimal | Extra pointer storage (8 bytes per node on 64‑bit) |
| Cache locality | Excellent (prefetching) | Poor (pointer chasing) |
| Dynamic sizing | Fixed or amortized resizing | Naturally dynamic |

**Interview tips**:
- Use array when you need frequent random access and know approximate size.
- Use linked list when you need frequent insertions/deletions at known positions (e.g., LRU cache).
- **Typical question**: Implement a linked list reversal, detect cycle, find middle.

## 2. Stack vs Queue vs Heap

| Feature | Stack (LIFO) | Queue (FIFO) | Heap (Priority Queue) |
|---------|--------------|--------------|------------------------|
| Access order | Last‑in‑first‑out | First‑in‑first‑out | By priority (min or max) |
| Typical O(1) ops | push, pop, top | enqueue, dequeue, front | getMin/getMax (O(1)), insert O(log n) |
| Implementation | Array, linked list | Circular array, linked list | Binary heap (array) |
| Use cases | Function calls, undo, parsing | BFS, scheduling, buffering | Dijkstra, Huffman coding, Kth largest |

**Interview tips**:
- **Stack**: Balanced parentheses, next greater element, evaluate postfix.
- **Queue**: Level order traversal, sliding window maximum (with deque).
- **Heap**: Merge K sorted lists, find median in stream.

## 3. Recursion vs Iteration

| Aspect | Recursion | Iteration |
|--------|-----------|-----------|
| Code clarity | Concise for naturally recursive problems (trees, divide‑and‑conquer) | More verbose but often easier to follow for simple loops |
| Performance | Function call overhead | No call overhead |
| Space complexity | O(depth) stack space | Usually O(1) extra space |
| Risk | Stack overflow for deep recursion | No stack overflow |
| Tail recursion | Can be optimised into iteration by compiler (not guaranteed) | Not applicable |

**When to use recursion**:
- Tree/graph traversals (DFS)
- Divide‑and‑conquer (merge sort, quick sort)
- Backtracking (N‑Queens, permutations)

**When to use iteration**:
- Deep recursion (n > 10^5)
- Performance‑critical loops
- When constant space is required

**Interview tip**: Often you are asked to implement both (e.g., Fibonacci, binary search, tree traversal). Know how to convert recursion to iteration using an explicit stack.

## 4. DFS vs BFS

| Feature | DFS | BFS |
|---------|-----|-----|
| Data structure | Stack (implicit call stack or explicit) | Queue |
| Space complexity | O(depth) – can be O(n) for skewed tree | O(width) – often larger for wide graphs |
| Shortest path (unweighted) | Finds a path, not guaranteed shortest | Guarantees shortest path in unweighted graphs |
| Cycle detection | Easy (recursion stack) | Possible but needs extra tracking |
| Topological sort | DFS‑based (postorder) | Kahn’s algorithm (BFS) |
| Best for | Connected components, puzzles (maze), solving constraints | Shortest path, web crawling, level order |

**Interview tips**:
- Use BFS for shortest path in grid (word ladder, number of islands distance).
- Use DFS for problems requiring exhaustive search (permutations, subsets) or when graph is deep but narrow.
- Be ready to implement both traversals on graphs and trees.

## 5. Hash Map vs Tree Map

| Feature | Hash Map (unordered_map) | Tree Map (map) |
|---------|--------------------------|----------------|
| Underlying structure | Hash table | Balanced BST (e.g., Red‑Black tree) |
| Average time for insert/search/delete | O(1) | O(log n) |
| Worst‑case time | O(n) (hash collisions) | O(log n) guaranteed |
| Ordering | No | Sorted by key |
| Memory overhead | Hash table load factor | Node pointers (left, right, color) |
| Use cases | Fast lookups, counting frequencies | Need ordered iteration, range queries, floor/ceiling |

**Interview tip**: In C++, `std::unordered_map` is hash map, `std::map` is tree map. Know when each is preferred. For range queries (e.g., count keys between L and R), tree map is essential.

## 6. Comparison of Sorting Algorithms

| Algorithm | Best | Average | Worst | Space | Stable | In‑place | Adaptive |
|-----------|------|---------|-------|-------|--------|----------|----------|
| Bubble | O(n) | O(n²) | O(n²) | O(1) | Yes | Yes | Yes |
| Selection | O(n²) | O(n²) | O(n²) | O(1) | No | Yes | No |
| Insertion | O(n) | O(n²) | O(n²) | O(1) | Yes | Yes | Yes |
| Merge | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes | No | No |
| Quick | O(n log n) | O(n log n) | O(n²) | O(log n) | No | Yes | No |
| Heap | O(n log n) | O(n log n) | O(n log n) | O(1) | No | Yes | No |
| Counting | O(n+k) | O(n+k) | O(n+k) | O(k) | Yes | No | No |
| Radix | O(nk) | O(nk) | O(nk) | O(n+k) | Yes | No | No |

**Stability** – equal elements preserve relative order. Important when sorting by multiple keys (e.g., sort by name, then by age).

**Interview tip**:
- Quick sort is often fastest in practice for arrays (good cache locality).
- Merge sort is stable and used for linked lists (no extra array overhead) and external sorting.
- Counting/Radix sort when integer range is limited (e.g., sorting 1 million ages 0‑120).

## 7. Singly vs Doubly Linked List

| Feature | Singly Linked List | Doubly Linked List |
|---------|--------------------|--------------------|
| Node structure | data + next | data + prev + next |
| Memory per node | Lower | Higher (extra pointer) |
| Reverse traversal | Not possible (without O(n) reversal) | O(1) backward |
| Deletion of a given node (without prev) | O(n) to find previous | O(1) using prev pointer |
| Insertion before a node | O(n) | O(1) |
| Typical use cases | Stack, queue, adjacency list | LRU cache, undo/redo, browser history |

**Interview tip**: Many problems (e.g., palindrome linked list, reverse in groups) are simpler with doubly linked list but must often be solved with singly linked list to test pointer manipulation.

## 8. Binary Search Tree vs Hash Table

| Feature | BST (balanced) | Hash Table |
|---------|----------------|------------|
| Average search/insert/delete | O(log n) | O(1) |
| Worst‑case (unbalanced/ collisions) | O(n) | O(n) |
| Ordering | Keys are sorted | No order |
| Range queries (find between L and R) | O(log n + k) | Not possible (requires full scan) |
| Predecessor / successor | O(log n) | Not supported |
| Memory | Node pointers | Load factor overhead |

**Interview tip**: Use hash table for exact lookups (dictionary). Use BST when ordering matters (e.g., all keys between x and y, find closest value). C++ `std::set` (ordered set) vs `std::unordered_set` (hash set).

## 9. When to Use DP vs Greedy vs Backtracking vs Divide and Conquer

| Paradigm | When to Use | Example |
|----------|-------------|---------|
| **Divide and Conquer** | Subproblems are independent, no overlap | Merge sort, closest pair, Karatsuba |
| **Dynamic Programming** | Overlapping subproblems + optimal substructure | Knapsack, LCS, edit distance |
| **Greedy** | Locally optimal choice leads to global optimum (greedy choice property) | Activity selection, fractional knapsack, Dijkstra |
| **Backtracking** | Need to explore all possibilities, constraint satisfaction | N‑Queens, Sudoku, permutations |

**Decision flow**:
1. Can you break into smaller independent problems? → D&C.
2. Do subproblems overlap? → DP (memoisation/tabulation).
3. Does a simple local choice always lead to optimum? → Greedy (test with counterexample).
4. Need to search all configurations? → Backtracking.

**Interview tip**: For optimisation problems (max/min), DP is often the answer unless greedy holds. For counting all solutions, backtracking.

## 10. Union‑Find (Disjoint Set Union) Applications

**What**: Data structure that tracks elements partitioned into disjoint sets. Supports `find` (which set?) and `union` (merge two sets) in nearly O(1) with path compression + union by rank.

**Applications**:
- **Kruskal’s MST algorithm** – detect cycles when adding edges.
- **Dynamic connectivity** – determine if two nodes are connected in an undirected graph after adding edges.
- **Number of connected components** in a graph.
- **Union‑find on grid** – connect adjacent cells (e.g., number of islands, regions).
- **Equivalence relation problems** – e.g., friends in a social network, grouping by common factors.

**Example** (union‑find on 2D grid to count islands – alternative to DFS):

```cpp
int find(vector<int>& parent, int x) {
    if (parent[x] != x) parent[x] = find(parent, parent[x]);
    return parent[x];
}
void unite(vector<int>& parent, vector<int>& rank, int x, int y) {
    int rx = find(parent, x), ry = find(parent, y);
    if (rx == ry) return;
    if (rank[rx] < rank[ry]) parent[rx] = ry;
    else if (rank[rx] > rank[ry]) parent[ry] = rx;
    else { parent[ry] = rx; rank[rx]++; }
}
```

**Interview tip**: Know the two optimisations – path compression and union by rank/size. Be able to implement DSU from scratch.

## 11. Trie vs Hash Table for String Search

| Feature | Trie | Hash Table |
|---------|------|-------------|
| Search exact string | O(L) where L = length | O(L) average (hash computation) |
| Search prefix / auto‑complete | O(L) to traverse | Not possible (would need to scan all keys) |
| Memory | Potentially high (many nodes) | Lower for few strings |
| Delete | O(L) | O(1) average |
| Space overhead | Node pointers per character | Hash table load factor |
| Use cases | Dictionary with prefix queries, IP routing | Exact lookups, frequency counting |

**When to use Trie**:
- Auto‑complete (prefix search)
- Spell checking (find words with small edit distance)
- Longest common prefix
- Word break problems (DP + trie)

**When to use Hash Table**:
- Simple existence check
- Counting word frequencies
- When prefixes are never needed

**Interview tip**: Many problems can be solved with both (e.g., word search, word break), but trie gives O(L) prefix operations and is often expected for prefix‑related tasks.

## 12. Two‑Pointer vs Sliding Window

| Feature | Two‑Pointer | Sliding Window |
|---------|-------------|----------------|
| Typical structure | Two pointers moving towards each other (opposite) or same direction at different speeds | Left and right pointers, window expands/contracts |
| Use cases | Palindromes, pair sum in sorted array, removing duplicates, merge sorted arrays | Subarray/substring problems with constraints (sum, distinct characters) |
| Window size | Fixed or variable (but usually not maintaining a range) | Variable or fixed, always a contiguous segment |
| Condition to move pointers | Usually based on comparison of values at both ends | Usually based on constraint (e.g., sum ≤ K, at most K distinct chars) |
| Time complexity | O(n) | O(n) |

**Examples**:
- **Two‑pointer opposite**: `isPalindrome`, `twoSum` in sorted array.
- **Two‑pointer same direction**: `removeDuplicates`, `findMiddle`.
- **Sliding window fixed size**: maximum sum of subarray size K.
- **Sliding window variable size**: longest substring without repeating characters.

**Interview tip**: Sliding window is a specialised two‑pointer technique where pointers define a contiguous window. Recognising which to use is key: if the answer requires a contiguous segment with a constraint → sliding window; if ordering of elements matters (e.g., checking palindrome, pair sum) → two‑pointer.

## Summary Table of Comparisons

| Comparison | Deciding Factor |
|------------|-----------------|
| Array vs Linked List | Need random access (array) vs frequent insert/delete at known positions (linked list) |
| Stack vs Queue vs Heap | Access order: LIFO, FIFO, or by priority |
| Recursion vs Iteration | Depth of recursion, code clarity, stack space |
| DFS vs BFS | Shortest path (BFS) vs exhaustive search (DFS) |
| Hash Map vs Tree Map | Need ordering (tree) vs faster average (hash) |
| Sorting algorithms | Input size, stability, in‑place requirement |
| Singly vs Doubly | Need backward traversal / O(1) delete given node |
| BST vs Hash Table | Range queries & ordering (BST) vs exact lookups (hash) |
| DP / Greedy / Backtracking / D&C | Overlap, optimal substructure, greedy choice |
| Union‑Find | Dynamic connectivity, cycle detection in Kruskal |
| Trie vs Hash Table | Prefix queries (trie) vs exact matches (hash) |
| Two‑pointer vs Sliding Window | Contiguous segment constraint (sliding window) vs pairwise or multi‑pointer (two‑pointer) |

Use this chapter as a quick reference before interviews to refresh key trade‑offs and problem‑solving patterns.
