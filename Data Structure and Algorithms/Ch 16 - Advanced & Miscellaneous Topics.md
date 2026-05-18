# Chapter 16: Advanced & Miscellaneous Topics

This chapter covers algorithms and data structures that appear frequently in intermediate to advanced coding interviews but do not fit neatly into other chapters. Topics include monotonic stack, deque for sliding window, ordered sets, rolling hash, majority vote algorithms, reservoir sampling, interval merging, meeting rooms II, and randomized algorithms.

## 1. Monotonic Stack

**What**: A stack that maintains elements in increasing or decreasing order. It is used to find the next greater (or smaller) element for each position in O(n) time.

### 1.1 Next Greater Element

**Problem**: For each element in an array, find the next element to the right that is greater.

**Algorithm**: Iterate from left to right, maintaining a decreasing stack (from bottom to top). For each new element, pop while stack top is smaller – the current element is the next greater for those popped indices.

```cpp
vector<int> nextGreaterElement(vector<int>& nums) {
    int n = nums.size();
    vector<int> result(n, -1);
    stack<int> st; // stores indices
    for (int i = 0; i < n; ++i) {
        while (!st.empty() && nums[st.top()] < nums[i]) {
            result[st.top()] = nums[i];
            st.pop();
        }
        st.push(i);
    }
    return result;
}
```

**Time**: O(n). **Space**: O(n).

**Real‑life analogy**: In a line of people, find the next taller person for each.

### 1.2 Largest Rectangle in Histogram

**Problem**: Given bar heights, find the largest rectangular area in the histogram.

**Approach**: Use a monotonic increasing stack (store indices with increasing heights). When a shorter bar is encountered, pop taller bars and calculate area with the popped bar as the smallest height.

```cpp
int largestRectangleArea(vector<int>& heights) {
    stack<int> st;
    int maxArea = 0;
    heights.push_back(0); // sentinel
    for (int i = 0; i < heights.size(); ++i) {
        while (!st.empty() && heights[st.top()] > heights[i]) {
            int h = heights[st.top()]; st.pop();
            int left = st.empty() ? -1 : st.top();
            maxArea = max(maxArea, h * (i - left - 1));
        }
        st.push(i);
    }
    heights.pop_back();
    return maxArea;
}
```

**Time**: O(n). **Space**: O(n).

## 2. Deque Applications – Sliding Window Maximum

**Problem**: Find the maximum in every contiguous subarray of size k.

**Approach**: Maintain a deque storing indices of candidate maximums. The deque is kept in decreasing order of values. For each new index `i`:
- Remove indices from front that are out of the window (`i - k`).
- Remove indices from back whose values are ≤ current value (they will never be maximum).
- Push current index.
- The front is the maximum for the window ending at `i` (when `i >= k-1`).

```cpp
vector<int> slidingWindowMaximum(vector<int>& nums, int k) {
    deque<int> dq;
    vector<int> result;
    for (int i = 0; i < nums.size(); ++i) {
        if (!dq.empty() && dq.front() == i - k) dq.pop_front();
        while (!dq.empty() && nums[dq.back()] <= nums[i]) dq.pop_back();
        dq.push_back(i);
        if (i >= k - 1) result.push_back(nums[dq.front()]);
    }
    return result;
}
```

**Time**: O(n). **Space**: O(k).

**Real‑life analogy**: A moving magnifying glass over a number line – you always keep the largest visible number at the front of the queue.

## 3. Multiset and Ordered Set (Balanced BST)

**What**: Data structures that maintain elements in sorted order and support insertion, deletion, and lookup in O(log n). In C++: `std::set` (unique keys) and `std::multiset` (allowing duplicates). Implemented as Red‑Black trees.

**Use cases**:
- Maintaining a running median (use two multisets or heaps).
- Order statistics (find kth smallest in dynamic set).
- Range queries (elements between L and R).

**Example: Running Median** using two multisets (max‑heap and min‑heap):

```cpp
void addNum(int num, multiset<int>& left, multiset<int>& right) {
    if (left.empty() || num <= *left.rbegin()) left.insert(num);
    else right.insert(num);
    if (left.size() > right.size() + 1) {
        right.insert(*left.rbegin());
        left.erase(prev(left.end()));
    } else if (right.size() > left.size()) {
        left.insert(*right.begin());
        right.erase(right.begin());
    }
}
double findMedian(multiset<int>& left, multiset<int>& right) {
    if (left.size() > right.size()) return *left.rbegin();
    return (*left.rbegin() + *right.begin()) / 2.0;
}
```

**Real‑life analogy**: A sorted list of exam scores that updates as new scores arrive – you always need the median quickly.

## 4. Rolling Hash (Rabin‑Karp)

**What**: A hashing technique that computes the hash of a sliding window in O(1) after O(n) preprocessing. Used for pattern matching.

**Polynomial rolling hash**:  
`hash(s) = Σ s[i] * p^i mod M`

When sliding the window, update:  
`new_hash = (old_hash - s[left] * p^(len-1)) * p + s[right+1]`

```cpp
#define MOD 1000000007
#define BASE 31

vector<int> rabinKarp(string text, string pattern) {
    int n = text.size(), m = pattern.size();
    if (m > n) return {};
    long long pHash = 0, tHash = 0, pow = 1;
    for (int i = 0; i < m; ++i) {
        pHash = (pHash * BASE + pattern[i]) % MOD;
        tHash = (tHash * BASE + text[i]) % MOD;
        if (i > 0) pow = (pow * BASE) % MOD;
    }
    vector<int> occurrences;
    for (int i = 0; i <= n - m; ++i) {
        if (pHash == tHash) {
            // double‑check actual characters to avoid false positives
            if (text.substr(i, m) == pattern) occurrences.push_back(i);
        }
        if (i < n - m) {
            tHash = (tHash - text[i] * pow % MOD + MOD) % MOD;
            tHash = (tHash * BASE + text[i+m]) % MOD;
        }
    }
    return occurrences;
}
```

**Time**: O(n+m) average. **Space**: O(1).

**Real‑life analogy**: Quickly checking if a fingerprint (pattern) appears in a long strip of paper – you slide a window and compare a compact signature, only verifying when signatures match.

## 5. Boyer‑Moore Majority Vote Algorithm

**Problem**: Find the majority element (element that appears more than ⌊n/2⌋ times) in O(n) time and O(1) space.

**Algorithm**:
1. **Candidate selection**: Pair up different elements and cancel them. The remaining candidate is the only possible majority element.
2. **Verification**: Count occurrences of the candidate to confirm.

```cpp
int majorityElement(vector<int>& nums) {
    int candidate = 0, count = 0;
    for (int x : nums) {
        if (count == 0) candidate = x;
        count += (x == candidate) ? 1 : -1;
    }
    // verification pass (optional if majority guaranteed)
    int freq = 0;
    for (int x : nums) if (x == candidate) freq++;
    return (freq > nums.size()/2) ? candidate : -1;
}
```

**Real‑life analogy**: In a battle, each pair of different fighters eliminates each other. The last survivor could be the one with the majority.

## 6. Reservoir Sampling

**Problem**: Randomly select k elements from a stream of unknown length (or very large) with equal probability.

**Algorithm**: For i < k, keep all first k elements. For i ≥ k, replace a random element with probability k/(i+1).

```cpp
vector<int> reservoirSample(vector<int>& stream, int k) {
    vector<int> reservoir(k);
    for (int i = 0; i < k; ++i) reservoir[i] = stream[i];
    for (int i = k; i < stream.size(); ++i) {
        int j = rand() % (i + 1);
        if (j < k) reservoir[j] = stream[i];
    }
    return reservoir;
}
```

**Proof of uniform probability**: Each element has probability k/n of being selected.

**Real‑life analogy**: Randomly selecting 10 songs from a streaming service that keeps adding new songs – you maintain a representative sample.

## 7. Interval Merging and Partitioning

**Problem**: Merge overlapping intervals.

**Approach**: Sort intervals by start time, then iterate and merge if current start ≤ last end.

```cpp
vector<pair<int,int>> mergeIntervals(vector<pair<int,int>>& intervals) {
    if (intervals.empty()) return {};
    sort(intervals.begin(), intervals.end());
    vector<pair<int,int>> merged;
    merged.push_back(intervals[0]);
    for (auto& [start, end] : intervals) {
        if (start <= merged.back().second) {
            merged.back().second = max(merged.back().second, end);
        } else {
            merged.push_back({start, end});
        }
    }
    return merged;
}
```

**Time**: O(n log n). **Space**: O(n).

**Real‑life analogy**: Merging overlapping calendar appointments.

## 8. Meeting Rooms II (Minimum Meeting Rooms Required)

**Problem**: Given intervals (start, end), find the minimum number of rooms needed to schedule all meetings without overlap.

**Approach 1 – Sweep line**: Count simultaneous meetings by sorting all events (start +1, end -1) and using cumulative sum.

```cpp
int minMeetingRooms(vector<pair<int,int>>& intervals) {
    vector<pair<int,int>> events; // (time, type): +1 for start, -1 for end
    for (auto& [s, e] : intervals) {
        events.emplace_back(s, 1);
        events.emplace_back(e, -1);
    }
    sort(events.begin(), events.end());
    int curr = 0, maxRooms = 0;
    for (auto& [time, delta] : events) {
        curr += delta;
        maxRooms = max(maxRooms, curr);
    }
    return maxRooms;
}
```

**Approach 2 – Two pointers** (sort starts and ends separately, similar to minimum platforms).

**Real‑life analogy**: Determining the peak number of simultaneous lectures in a university.

## 9. Randomized Algorithms

Randomized algorithms use random numbers to simplify or speed up solutions. They often run faster on average and have small probability of error (or deterministic with high probability).

### 9.1 Quickselect (Randomized Selection)

**Problem**: Find the kth smallest element in unsorted array.

**Approach**: Randomly choose a pivot, partition the array, then recurse into one side.

```cpp
int quickselect(vector<int>& nums, int left, int right, int k) {
    if (left == right) return nums[left];
    int pivotIdx = left + rand() % (right - left + 1);
    swap(nums[pivotIdx], nums[right]);
    int i = left - 1;
    for (int j = left; j < right; ++j)
        if (nums[j] <= nums[right]) swap(nums[++i], nums[j]);
    swap(nums[i+1], nums[right]);
    if (k == i+1) return nums[k];
    else if (k < i+1) return quickselect(nums, left, i, k);
    else return quickselect(nums, i+2, right, k);
}
```

**Expected time**: O(n). **Worst case**: O(n²) if pivots are always bad (rare with randomness).

### 9.2 Randomized Quicksort

Same as quicksort but the pivot is chosen randomly. This eliminates the worst‑case O(n²) for sorted input. Expected O(n log n).

## 10. Summary Table

| Topic | Core Idea | Time | Space | Use Case |
|-------|-----------|------|-------|----------|
| Monotonic stack | Maintain order to find next greater/smaller | O(n) | O(n) | Largest rectangle, stock span |
| Deque for sliding window | Maintain indices in decreasing order | O(n) | O(k) | Sliding window max/min |
| Multiset / ordered set | Balanced BST | O(log n) per op | O(n) | Running median, order stats |
| Rolling hash (Rabin‑Karp) | Polynomial hash sliding | O(n+m) avg | O(1) | Pattern matching, plagiarism detection |
| Boyer‑Moore majority | Pair cancellation | O(n) | O(1) | Majority element (freq > n/2) |
| Reservoir sampling | Random replacement | O(n) | O(k) | Sample from stream |
| Interval merging | Sort by start, merge | O(n log n) | O(n) | Overlap merging |
| Meeting Rooms II | Sweep line (event count) | O(n log n) | O(n) | Min rooms / platforms |
| Quickselect | Randomized partition | O(n) expected | O(log n) | kth smallest |
| Randomized quicksort | Random pivot | O(n log n) expected | O(log n) | General sorting |

These advanced topics are often the difference between a good solution and an optimal one in coding interviews. Practice implementing each from scratch to build fluency.
