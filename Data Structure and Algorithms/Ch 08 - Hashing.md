# Chapter 8: Hashing

Hashing provides near‑constant‑time insertion, deletion, and lookup by mapping keys to array indices using a hash function. This chapter covers hash functions, collision resolution strategies, load factor, rehashing, implementations of hash maps and sets, and classic applications.

## 1. Hash Functions

**What**: A function that maps a key (integer, string, or any object) to an integer index within a fixed range `[0, m‑1]`.

**Desirable properties**:
- **Deterministic**: Same key always produces the same hash.
- **Fast to compute**: O(1) or O(len(key)).
- **Uniform distribution**: Minimises collisions by spreading keys evenly.
- **Minimises collisions**: Different keys should rarely map to the same index.

**Simple examples**:
- Integer keys: `hash(key) = key % m` (choose `m` as a prime number to improve distribution).
- String keys: polynomial rolling hash `hash = (hash * BASE + char) % m`.

```cpp
// Simple integer hash
int hashInt(int key, int m) { return key % m; }

// Polynomial rolling hash for strings
int hashString(const string& key, int m) {
    const int BASE = 31;
    long long hash = 0;
    for (char c : key) hash = (hash * BASE + c) % m;
    return (int)hash;
}
```

**Real-life analogy**: Library classification. A book’s title (key) is mapped to a shelf number (hash). Good classification distributes books evenly across shelves.

## 2. Collision Resolution

A collision occurs when two different keys hash to the same index.

### 2.1 Chaining (Separate Chaining)

**What**: Each bucket contains a linked list (or dynamic array) of key‑value pairs that hash to that bucket.

**Operations**:
- Insert: hash to bucket, add to list (check for duplicates if needed).
- Search: hash to bucket, traverse list.
- Delete: hash to bucket, remove from list.

**Performance**:
- Average: O(1 + α) where α = n/m (load factor).
- Worst case (all keys in one bucket): O(n).

```cpp
template<typename K, typename V>
class HashMapChaining {
    struct Node { K key; V value; Node* next; };
    vector<Node*> buckets;
    int size, capacity;
    int hash(K key) { return key % capacity; }
public:
    HashMapChaining(int cap = 101) : capacity(cap), size(0) {
        buckets.resize(capacity, nullptr);
    }
    void insert(K key, V value) {
        int idx = hash(key);
        Node* curr = buckets[idx];
        while (curr) {
            if (curr->key == key) { curr->value = value; return; }
            curr = curr->next;
        }
        Node* newNode = new Node{key, value, buckets[idx]};
        buckets[idx] = newNode;
        size++;
    }
    bool find(K key, V& out) {
        int idx = hash(key);
        Node* curr = buckets[idx];
        while (curr) {
            if (curr->key == key) { out = curr->value; return true; }
            curr = curr->next;
        }
        return false;
    }
    // delete, destructor omitted for brevity
};
```

**When to use**: Most general purpose; handles high load factor well.

### 2.2 Open Addressing

**What**: All entries are stored in the array itself. When a collision occurs, the table is probed to find an empty slot.

**Probing sequences**:

- **Linear probing**: `index = (hash + i) % m` for i = 0,1,2,...
  - Advantages: Cache friendly.
  - Disadvantage: Primary clustering → long runs of occupied slots.

- **Quadratic probing**: `index = (hash + c1*i + c2*i²) % m`.
  - Reduces clustering but may not probe all slots.

- **Double hashing**: `index = (hash1 + i * hash2(key)) % m`, where `hash2` is a second hash function.
  - Provides good distribution, avoids clustering.

**Performance**: Sensitive to load factor; typically keep α < 0.7.

```cpp
class HashMapOpenAddressing {
    vector<pair<int, int>> table;
    vector<bool> occupied, deleted; // deleted flag for lazy deletion
    int capacity, size;
    int hash1(int key) { return key % capacity; }
    int hash2(int key) { return 1 + (key % (capacity - 1)); }
public:
    HashMapOpenAddressing(int cap = 101) : capacity(cap), size(0) {
        table.resize(capacity);
        occupied.resize(capacity, false);
        deleted.resize(capacity, false);
    }
    void insert(int key, int value) {
        int idx = hash1(key);
        int step = hash2(key);
        for (int i = 0; i < capacity; ++i) {
            int probe = (idx + i * step) % capacity;
            if (!occupied[probe] || deleted[probe]) {
                table[probe] = {key, value};
                occupied[probe] = true;
                deleted[probe] = false;
                size++;
                return;
            }
            if (occupied[probe] && table[probe].first == key) {
                table[probe].second = value; // update
                return;
            }
        }
        // table full – rehash needed
    }
    // find and erase similar
};
```

## 3. Load Factor and Rehashing

**Load factor** α = number of entries / table size.

- For chaining, α > 1 is acceptable (average chain length = α).
- For open addressing, keep α < 0.7 to avoid excessive probing.

**Rehashing**: When α exceeds a threshold (e.g., 0.75), allocate a larger table (usually double size) and re‑insert all entries using the new hash function.

```cpp
void rehash() {
    int newCapacity = capacity * 2;
    vector<pair<int, int>> oldTable = table;
    vector<bool> oldOccupied = occupied;
    capacity = newCapacity;
    table.assign(capacity, {0,0});
    occupied.assign(capacity, false);
    deleted.assign(capacity, false);
    size = 0;
    for (int i = 0; i < oldTable.size(); ++i) {
        if (oldOccupied[i] && !deleted[i])
            insert(oldTable[i].first, oldTable[i].second);
    }
}
```

## 4. Hash Map and Hash Set Implementations

### 4.1 Hash Map (Dictionary)

Stores key‑value pairs. C++ `std::unordered_map` (average O(1) operations).

### 4.2 Hash Set

Stores only keys (no values). C++ `std::unordered_set`.

**Simple hash set using chaining**:

```cpp
class HashSet {
    vector<list<int>> buckets;
    int hash(int key) { return key % buckets.size(); }
public:
    HashSet(int cap = 101) : buckets(cap) {}
    void add(int key) {
        int idx = hash(key);
        for (int x : buckets[idx]) if (x == key) return;
        buckets[idx].push_back(key);
    }
    bool contains(int key) {
        int idx = hash(key);
        for (int x : buckets[idx]) if (x == key) return true;
        return false;
    }
    void remove(int key) {
        int idx = hash(key);
        buckets[idx].remove(key);
    }
};
```

## 5. Applications

### 5.1 Two‑Sum Problem

**Problem**: Given an array of integers and a target, return indices of two numbers that add to target.

**Approach**: Use a hash map from value to index. For each element `nums[i]`, check if `target - nums[i]` exists in the map.

```cpp
vector<int> twoSum(vector<int>& nums, int target) {
    unordered_map<int, int> m; // value -> index
    for (int i = 0; i < nums.size(); ++i) {
        int complement = target - nums[i];
        if (m.find(complement) != m.end())
            return {m[complement], i};
        m[nums[i]] = i;
    }
    return {};
}
```

**Time**: O(n). **Space**: O(n).

### 5.2 Subarray Sum Equals K

**Problem**: Count number of contiguous subarrays whose sum equals k.

**Approach**: Use prefix sum and a hash map storing frequency of each prefix sum. For each prefix sum `curr`, add the count of `curr - k` seen so far.

```cpp
int subarraySum(vector<int>& nums, int k) {
    unordered_map<int, int> freq;
    freq[0] = 1; // empty prefix sum
    int prefix = 0, count = 0;
    for (int x : nums) {
        prefix += x;
        count += freq[prefix - k];
        freq[prefix]++;
    }
    return count;
}
```

**Time**: O(n). **Space**: O(n).

### 5.3 Longest Consecutive Sequence

**Problem**: Find the length of the longest consecutive elements sequence in unsorted array (O(n) time).

**Approach**: Insert all numbers into a hash set. For each number, if its predecessor (`num-1`) is not in the set, it is the start of a sequence. Then count consecutive numbers.

```cpp
int longestConsecutive(vector<int>& nums) {
    unordered_set<int> s(nums.begin(), nums.end());
    int best = 0;
    for (int x : nums) {
        if (s.find(x - 1) == s.end()) {
            int len = 1;
            while (s.find(x + len) != s.end()) len++;
            best = max(best, len);
        }
    }
    return best;
}
```

**Time**: O(n) (each element visited at most twice). **Space**: O(n).

### 5.4 Group Anagrams

**Problem**: Group strings that are anagrams of each other.

**Approach**: For each string, sort its characters to form a key, or use a frequency count as key.

```cpp
vector<vector<string>> groupAnagrams(vector<string>& strs) {
    unordered_map<string, vector<string>> groups;
    for (string s : strs) {
        string key = s;
        sort(key.begin(), key.end());
        groups[key].push_back(s);
    }
    vector<vector<string>> result;
    for (auto& p : groups) result.push_back(p.second);
    return result;
}
```

**Time**: O(n * k log k) where k is max string length. **Space**: O(nk).

### 5.5 LRU Cache (Hash Map + Doubly Linked List)

**Problem**: Design a cache that evicts the least recently used item when capacity is exceeded.

**Approach**: 
- Hash map: key → node pointer (for O(1) access).
- Doubly linked list: nodes in order of recent use (most recent at head, least at tail).

**Operations**:
- `get(key)`: if key exists, move node to head, return value.
- `put(key, value)`: if key exists, update value and move to head; else insert new node at head; if over capacity, remove tail.

```cpp
class LRUCache {
    struct Node {
        int key, val;
        Node *prev, *next;
        Node(int k, int v) : key(k), val(v), prev(nullptr), next(nullptr) {}
    };
    unordered_map<int, Node*> m;
    Node *head, *tail;
    int cap, size;

    void addToHead(Node* node) {
        node->next = head->next;
        node->prev = head;
        head->next->prev = node;
        head->next = node;
    }
    void removeNode(Node* node) {
        node->prev->next = node->next;
        node->next->prev = node->prev;
    }
    void moveToHead(Node* node) {
        removeNode(node);
        addToHead(node);
    }
    Node* removeTail() {
        Node* node = tail->prev;
        removeNode(node);
        return node;
    }
public:
    LRUCache(int capacity) : cap(capacity), size(0) {
        head = new Node(-1, -1);
        tail = new Node(-1, -1);
        head->next = tail;
        tail->prev = head;
    }
    int get(int key) {
        if (m.find(key) == m.end()) return -1;
        Node* node = m[key];
        moveToHead(node);
        return node->val;
    }
    void put(int key, int value) {
        if (m.find(key) != m.end()) {
            Node* node = m[key];
            node->val = value;
            moveToHead(node);
            return;
        }
        Node* newNode = new Node(key, value);
        m[key] = newNode;
        addToHead(newNode);
        size++;
        if (size > cap) {
            Node* toRemove = removeTail();
            m.erase(toRemove->key);
            delete toRemove;
            size--;
        }
    }
};
```

**Time**: O(1) per operation. **Space**: O(capacity).

**Real-life analogy**: A librarian keeps frequently borrowed books on a shelf near the entrance (most recent). When new books arrive, the least recently borrowed book is moved to storage.

## 6. Summary

| Concept | Key Points |
|---------|-------------|
| Hash function | Maps key to index; uniform distribution reduces collisions |
| Chaining | Simple, handles α > 1; uses linked lists per bucket |
| Open addressing | Stores all entries in array; uses probing sequences |
| Load factor | n/m; rehash when exceeding threshold (e.g., 0.75) |
| Hash map / set | Average O(1) operations; `unordered_map` / `unordered_set` in C++ |
| Two‑sum | Hash map stores seen values |
| Subarray sum = K | Prefix sum + frequency map |
| Longest consecutive | Hash set enables O(n) sequence detection |
| Group anagrams | Sorted string or frequency count as key |
| LRU Cache | Hash map + doubly linked list gives O(1) get/put |

The next chapter will cover binary trees, binary search trees (BST), AVL trees, and tree traversals.
