# Chapter 12: Dynamic Programming (DP)

Dynamic Programming is a method for solving complex problems by breaking them into smaller overlapping subproblems and storing the results of each subproblem to avoid redundant computation. This chapter covers DP fundamentals, common mistakes, pattern recognition, when NOT to use DP, classic DP problems, subsequence and substring problems, knapsack, DP on strings, trees, bitmask DP, and Kadane’s algorithm as a DP view.

## 1. DP Fundamentals

### 1.1 Key Concepts

- **Overlapping Subproblems**: The problem can be broken into subproblems that are reused multiple times. Example: Fibonacci: F(n) = F(n-1) + F(n-2) recomputes the same values.
- **Optimal Substructure**: An optimal solution can be constructed from optimal solutions of its subproblems. Example: Shortest path from A to C passing through B – the path A→B and B→C must be optimal.
- **Memoization (Top‑Down)**: Recursive approach with caching. Solve the problem recursively and store results before returning.
- **Tabulation (Bottom‑Up)**: Iterative approach. Build a table from the smallest subproblem upwards.

### 1.2 Real‑Life Analogy

- **Memoization**: Taking notes during an exam. When you solve a problem, you write down the answer so that if it appears again in a different part, you just look it up.
- **Tabulation**: Building a table of times tables row by row; each new row uses previously computed rows.

### 1.3 Fibonacci Example

**Memoization (Top‑Down)**:

```cpp
vector<long long> memo(100, -1);
long long fibMemo(int n) {
    if (n <= 1) return n;
    if (memo[n] != -1) return memo[n];
    return memo[n] = fibMemo(n-1) + fibMemo(n-2);
}
```

**Tabulation (Bottom‑Up)**:

```cpp
long long fibTab(int n) {
    if (n <= 1) return n;
    vector<long long> dp(n+1);
    dp[0] = 0; dp[1] = 1;
    for (int i = 2; i <= n; ++i)
        dp[i] = dp[i-1] + dp[i-2];
    return dp[n];
}
```

**Space‑Optimised**:

```cpp
long long fibOpt(int n) {
    if (n <= 1) return n;
    int a = 0, b = 1, c;
    for (int i = 2; i <= n; ++i) {
        c = a + b;
        a = b;
        b = c;
    }
    return b;
}
```

## 2. Common DP Mistakes

Even with a correct recurrence, DP solutions often fail due to implementation pitfalls. Recognising these mistakes improves debugging and interview performance.

| Mistake | Description | Example | Correct Approach |
|---------|-------------|---------|-------------------|
| **Incorrect initialisation** | Base cases or DP table initial values are wrong. | In LCS, initialising `dp[0][j] = 1` instead of 0. | `dp[0][j] = 0` (empty prefix has no common subsequence). |
| **Out‑of‑order iteration** | In tabulation, traversing inner loop in wrong direction for 1D knapsack. | `for (int w = 0; w <= W; ++w)` for 0/1 knapsack – reuses same item multiple times. | Iterate `w` from `W` down to `weight[i]`. |
| **Off‑by‑one indices** | Using `dp[i]` when `i` should represent length or index incorrectly. | `dp[n]` accessed when `dp` size is `n`. | Use `dp[n+1]` when state is array length. |
| **Missing handling of impossible states** | Using `INT_MAX` without checking overflow. | `dp[i] = min(dp[i-1], dp[i-2]) + cost` without guarding `INT_MAX`. | Use `INT_MAX/2` for additions, check if `dp[i-1] != INT_MAX/2`. |
| **Using recursive memoization without clearing cache** | Global memo array reused across multiple test cases without resetting. | `memo` retains values from previous call. | Reset or use local memo per call. |
| **Forgetting to store computed result** | Recursive function returns value but does not memoise before returning. | `return fib(n-1) + fib(n-2)` without storing in `memo[n]`. | Store before returning. |
| **Using the wrong DP dimension** | Too few dimensions lose necessary state (e.g., knapsack with two constraints needs 2D). | `dp[W]` for knapsack with both weight and volume constraints. | Use `dp[W][V]`. |
| **Premature pruning of subproblems** | Skipping some states due to incorrect dominance assumption. | In subset sum, assuming larger sum is always better. | Evaluate all reachable states. |

### Example: Off‑by‑One Error in Climbing Stairs

**Incorrect**:
```cpp
int climbStairs(int n) {
    vector<int> dp(n, 0);
    dp[0] = 1;
    dp[1] = 2; // dp[1] accessed when n==1 -> out of bounds
    for (int i = 2; i < n; ++i) dp[i] = dp[i-1] + dp[i-2];
    return dp[n-1];
}
```

**Correct**:
```cpp
int climbStairs(int n) {
    if (n <= 2) return n;
    vector<int> dp(n+1);
    dp[1] = 1; dp[2] = 2;
    for (int i = 3; i <= n; ++i) dp[i] = dp[i-1] + dp[i-2];
    return dp[n];
}
```

## 3. DP Pattern Recognition

Identifying that a problem can be solved with DP is often the hardest step. The following patterns and questions help recognise DP problems during interviews or coding contests.

### 3.1 Key Questions to Ask

- **Can the problem be broken into smaller subproblems?** Does solving for input size `n` depend on solutions for smaller inputs (e.g., `n-1`, `n/2`)?
- **Are there overlapping subproblems?** Would a naive recursive solution recompute the same inputs many times?
- **Does the problem ask for optimisation?** (maximum, minimum, longest, shortest, number of ways, true/false).
- **Does the problem involve sequences, grids, or subsets?** Common DP domains.
- **Is the problem a variant of classic DP?** (LCS, knapsack, edit distance, coin change, etc.)

### 3.2 Quick Pattern Cheat Sheet

| Problem Characteristics | Likely DP Category | State Definition Example |
|-------------------------|--------------------|---------------------------|
| Sequence of decisions (take/skip, buy/sell) | 1D DP | `dp[i]` = best answer for first i elements |
| Grid path (right/down moves) | 2D grid DP | `dp[i][j]` = answer for cell (i,j) |
| Two strings comparison | String DP (LCS, edit distance) | `dp[i][j]` = answer for prefixes s1[0..i-1], s2[0..j-1] |
| Subset sum / knapsack | 0/1 Knapsack | `dp[w]` = max value for capacity w |
| Counting ways (without order) | Combination DP | `dp[x]` = number of ways to achieve amount x |
| Minimising partitions | Partition DP (palindrome, matrix chain) | `dp[i]` = min cost for prefix up to i |
| Tree with parent‑child dependencies | Tree DP | `dp[u][0/1]` = answer for subtree (node selected or not) |
| Small constraints (n ≤ 20) | Bitmask DP | `dp[mask][i]` = answer for visited set `mask` ending at i |
| Probability / expectation | Probabilistic DP | `dp[i]` = expected value from state i |

### 3.3 Example Recognition Walkthrough

**Problem**: Given an array of integers, find the length of the longest increasing subsequence.

- **Question**: Can we solve for prefix `i` using smaller prefixes? Yes: LIS ending at `i` depends on all previous `j < i` with `nums[j] < nums[i]`.
- **Overlapping subproblems?** Different `i` may consider the same `j` multiple times – yes.
- **Optimisation?** Yes, longest.
- **Classic pattern?** LIS – known DP with O(n²) or patience sorting.

**Result**: Use DP.

### 3.4 Transition from Brute‑Force to DP

1. Write a recursive backtracking solution that explores all possibilities.
2. Identify parameters that change during recursion.
3. Use those parameters as state dimensions.
4. Memoise results on those parameters.
5. (Optional) Convert to iterative tabulation.

## 4. When NOT to Use DP

DP is powerful, but it is not always the best or necessary tool. Recognising when other techniques are simpler or more efficient saves time and complexity.

### 4.1 Greedy Works Better

If a problem exhibits the **greedy choice property** (making the locally optimal choice leads to a global optimum), greedy is often simpler and faster (O(n) or O(n log n) vs DP’s potential O(n²) or higher).

**Examples**:
- **Coin change** (canonical coin systems like US coins): Greedy works. DP only needed for arbitrary denominations.
- **Activity selection** (maximise number of non‑overlapping intervals): Greedy by earliest finish time.
- **Minimum number of jumps to end** (when each jump length is limited): Greedy works in O(n).
- **Fractional knapsack**: Greedy by value/weight ratio. 0/1 knapsack requires DP.

**How to recognise**: Greedy works when selecting an item does not restrict future choices in a way that requires considering all subsets. Often the problem specifies “choose as many as possible” or “maximise” with no dependency on previously chosen items’ exact sum.

### 4.2 Sliding Window Is Sufficient

If the problem asks for a **contiguous subarray or substring** optimisation (length, sum, maximum) and the constraint involves a monotonic condition (e.g., at most K distinct characters, sum ≤ K), sliding window gives O(n) time and O(1) space – much better than DP.

**Examples**:
- **Longest substring with at most K distinct characters**: Sliding window.
- **Minimum size subarray sum**: Sliding window.
- **Maximum sum subarray of fixed size k**: Sliding window (or prefix sums).
- **Fruit into baskets** (max two types): Sliding window.

**How to recognise**: “Contiguous”, “subarray”, “substring” with a constraint that can be maintained by expanding/shrinking a window. DP would over‑complicate (e.g., O(n²) unnecessary).

### 4.3 Binary Search Optimization Is Possible

For problems that ask for **minimum of maximum** or **maximum of minimum** (or similar monotonic predicates), binary search on the answer combined with a feasibility check (often O(n) or O(n log n)) can be simpler than DP.

**Examples**:
- **Split array largest sum**: Minimise the largest sum of m subarrays. Binary search + greedy check.
- **Koko eating bananas**: Find minimum speed to eat all bananas within H hours. Binary search + simulation.
- **Capacity to ship packages within D days**: Binary search + greedy.
- **Median of two sorted arrays**: Binary search on smaller array.

**How to recognise**: The answer is a single value, and you can test in O(n) whether a candidate answer is feasible. The function `isFeasible(x)` is monotonic (false for small x, true for larger x). DP would likely be overkill or too slow.

### 4.4 Mathematical or Combinatorial Formula Exists

Some problems have a closed‑form solution (O(1)) or simple combinatorial formula, making DP unnecessary.

**Examples**:
- **Number of ways to reach the top of n steps** (with 1 or 2 steps) → Fibonacci (can be DP or Binet’s formula).
- **Unique paths in grid** – closed form using factorials: C(m+n-2, m-1).
- **Nth Catalan number** – formula exists, but DP is still common for understanding.

**How to recognise**: Problem asks for a pure count or specific value that matches a known sequence.

### 4.5 Important Caveat

DP may still be **correct** in all these cases, but it often leads to higher time/space complexity and more code. The table below summarises the decision:

| Technique | When to Use | Typical Complexity | DP Alternative Complexity |
|-----------|-------------|--------------------|---------------------------|
| Greedy | Problem has greedy choice property | O(n) or O(n log n) | O(n²) or higher |
| Sliding Window | Contiguous subarray with monotonic condition | O(n) | O(n²) (e.g., longest palindromic substring DP) |
| Binary Search on Answer | Minimise max / maximise min with monotonic feasibility | O(n log M) | Often O(n²) or exponential |
| Math Formula | Direct closed‑form exists | O(1) | O(n) or O(n²) |

**General rule**: If you suspect a greedy or sliding window solution, test it on small examples. If it holds, skip DP. If you are asked for “all possible” results, DP (or backtracking) is likely needed.

## 5. Classic DP Problems

### 5.1 Climbing Stairs

**Problem**: Count ways to reach the top of n steps by taking 1 or 2 steps at a time.

**DP Relation**: `dp[i] = dp[i-1] + dp[i-2]` with `dp[0]=1, dp[1]=1`.

```cpp
int climbStairs(int n) {
    if (n <= 1) return 1;
    int a = 1, b = 1, c;
    for (int i = 2; i <= n; ++i) {
        c = a + b;
        a = b;
        b = c;
    }
    return b;
}
```

### 5.2 House Robber (1D DP)

**Problem**: Maximise sum of non‑adjacent elements.

**DP Relation**: `dp[i] = max(dp[i-1], dp[i-2] + nums[i])`.

```cpp
int rob(vector<int>& nums) {
    int n = nums.size();
    if (n == 0) return 0;
    if (n == 1) return nums[0];
    int prev2 = nums[0], prev1 = max(nums[0], nums[1]);
    for (int i = 2; i < n; ++i) {
        int curr = max(prev1, prev2 + nums[i]);
        prev2 = prev1;
        prev1 = curr;
    }
    return prev1;
}
```

### 5.3 Minimum Path Sum (Grid)

**Problem**: Find path from top‑left to bottom‑right minimising sum (only right/down moves).

**DP**: `dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])`.

```cpp
int minPathSum(vector<vector<int>>& grid) {
    int m = grid.size(), n = grid[0].size();
    vector<vector<int>> dp(m, vector<int>(n));
    dp[0][0] = grid[0][0];
    for (int i = 1; i < m; ++i) dp[i][0] = dp[i-1][0] + grid[i][0];
    for (int j = 1; j < n; ++j) dp[0][j] = dp[0][j-1] + grid[0][j];
    for (int i = 1; i < m; ++i)
        for (int j = 1; j < n; ++j)
            dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1]);
    return dp[m-1][n-1];
}
```

### 5.4 Unique Paths (Grid)

**Problem**: Number of distinct paths from top‑left to bottom‑right (right/down moves).

**DP**: `dp[i][j] = dp[i-1][j] + dp[i][j-1]`.

```cpp
int uniquePaths(int m, int n) {
    vector<int> dp(n, 1);
    for (int i = 1; i < m; ++i)
        for (int j = 1; j < n; ++j)
            dp[j] += dp[j-1];
    return dp[n-1];
}
```

## 6. Subsequence and Substring Problems

### 6.1 Longest Common Subsequence (LCS)

**Problem**: Maximum length of common subsequence (not necessarily contiguous).

**DP Relation**:

```
dp[i][j] = dp[i-1][j-1] + 1                 if s1[i-1] == s2[j-1]
         = max(dp[i-1][j], dp[i][j-1])      otherwise
```

```cpp
int longestCommonSubsequence(string s1, string s2) {
    int m = s1.size(), n = s2.size();
    vector<vector<int>> dp(m+1, vector<int>(n+1, 0));
    for (int i = 1; i <= m; ++i)
        for (int j = 1; j <= n; ++j)
            if (s1[i-1] == s2[j-1])
                dp[i][j] = dp[i-1][j-1] + 1;
            else
                dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
    return dp[m][n];
}
```

### 6.2 Longest Common Substring

**DP**: `dp[i][j] = dp[i-1][j-1] + 1` if match, else 0. Track maximum.

### 6.3 Longest Increasing Subsequence (LIS)

**Problem**: Length of longest increasing subsequence.

**DP O(n²)**:

```cpp
int lengthOfLIS(vector<int>& nums) {
    int n = nums.size();
    vector<int> dp(n, 1);
    int best = 1;
    for (int i = 1; i < n; ++i) {
        for (int j = 0; j < i; ++j)
            if (nums[j] < nums[i])
                dp[i] = max(dp[i], dp[j] + 1);
        best = max(best, dp[i]);
    }
    return best;
}
```

**O(n log n) with patience sorting**:

```cpp
int lengthOfLIS(vector<int>& nums) {
    vector<int> tails;
    for (int x : nums) {
        auto it = lower_bound(tails.begin(), tails.end(), x);
        if (it == tails.end()) tails.push_back(x);
        else *it = x;
    }
    return tails.size();
}
```

### 6.4 Edit Distance (Levenshtein Distance)

**Problem**: Minimum number of insertions, deletions, substitutions to convert string A to B.

**DP Relation**:

```
dp[i][j] = dp[i-1][j-1]                     if A[i-1] == B[j-1]
         = 1 + min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]) otherwise
```

```cpp
int minDistance(string word1, string word2) {
    int m = word1.size(), n = word2.size();
    vector<vector<int>> dp(m+1, vector<int>(n+1));
    for (int i = 0; i <= m; ++i) dp[i][0] = i;
    for (int j = 0; j <= n; ++j) dp[0][j] = j;
    for (int i = 1; i <= m; ++i)
        for (int j = 1; j <= n; ++j)
            if (word1[i-1] == word2[j-1])
                dp[i][j] = dp[i-1][j-1];
            else
                dp[i][j] = 1 + min({dp[i-1][j], dp[i][j-1], dp[i-1][j-1]});
    return dp[m][n];
}
```

## 7. Subset and Knapsack Problems

### 7.1 0/1 Knapsack

**Problem**: Maximise value with capacity W, each item taken at most once.

**DP**: `dp[w] = max value achievable with capacity w`.

```cpp
int knapsack01(vector<int>& weights, vector<int>& values, int W) {
    int n = weights.size();
    vector<int> dp(W+1, 0);
    for (int i = 0; i < n; ++i)
        for (int w = W; w >= weights[i]; --w)
            dp[w] = max(dp[w], dp[w - weights[i]] + values[i]);
    return dp[W];
}
```

### 7.2 Subset Sum

**Problem**: Determine if a subset sums to a given target.

```cpp
bool subsetSum(vector<int>& nums, int target) {
    vector<bool> dp(target+1, false);
    dp[0] = true;
    for (int x : nums)
        for (int s = target; s >= x; --s)
            if (dp[s - x]) dp[s] = true;
    return dp[target];
}
```

### 7.3 Partition Equal Subset Sum

**Problem**: Can array be partitioned into two subsets with equal sum?

**Approach**: Check if subset sum exists for total/2.

```cpp
bool canPartition(vector<int>& nums) {
    int sum = accumulate(nums.begin(), nums.end(), 0);
    if (sum % 2) return false;
    return subsetSum(nums, sum/2);
}
```

## 8. DP on Strings

### 8.1 Palindrome Partitioning (Minimum Cuts)

**Problem**: Minimum cuts to partition a string into palindromes.

**DP**: Precompute palindromic substrings. Then `dp[i] = min cuts for prefix s[0..i]`.

```cpp
int minCut(string s) {
    int n = s.size();
    vector<vector<bool>> isPal(n, vector<bool>(n, false));
    for (int len = 1; len <= n; ++len)
        for (int i = 0; i + len - 1 < n; ++i) {
            int j = i + len - 1;
            if (s[i] == s[j] && (len <= 2 || isPal[i+1][j-1]))
                isPal[i][j] = true;
        }
    vector<int> dp(n, INT_MAX);
    for (int i = 0; i < n; ++i) {
        if (isPal[0][i]) dp[i] = 0;
        else {
            for (int j = 0; j < i; ++j)
                if (isPal[j+1][i])
                    dp[i] = min(dp[i], dp[j] + 1);
        }
    }
    return dp[n-1];
}
```

### 8.2 Wildcard Matching

**Problem**: Match pattern containing `?` (single char) and `*` (any sequence) with a string.

**DP**: `dp[i][j] = true if s[0..i-1] matches p[0..j-1]`.

```cpp
bool isMatch(string s, string p) {
    int m = s.size(), n = p.size();
    vector<vector<bool>> dp(m+1, vector<bool>(n+1, false));
    dp[0][0] = true;
    for (int j = 1; j <= n; ++j)
        if (p[j-1] == '*') dp[0][j] = dp[0][j-1];
    for (int i = 1; i <= m; ++i)
        for (int j = 1; j <= n; ++j)
            if (p[j-1] == '*' && (dp[i-1][j] || dp[i][j-1])) dp[i][j] = true;
            else if (p[j-1] == '?' || s[i-1] == p[j-1])
                dp[i][j] = dp[i-1][j-1];
    return dp[m][n];
}
```

### 8.3 Regular Expression Matching

Similar but with `*` meaning zero or more of the preceding character.

## 9. DP on Trees

### Maximum Independent Set in Tree (no two adjacent selected)

**DP**: For each node, compute `dp[node][0]` = max sum when node NOT selected, `dp[node][1]` = selected.

```
dp[node][0] = sum over children of max(dp[child][0], dp[child][1])
dp[node][1] = node.value + sum over children of dp[child][0]
```

```cpp
void dfs(int u, int parent, vector<vector<int>>& adj, vector<int>& val, vector<vector<int>>& dp) {
    dp[u][1] = val[u];
    dp[u][0] = 0;
    for (int v : adj[u]) {
        if (v == parent) continue;
        dfs(v, u, adj, val, dp);
        dp[u][0] += max(dp[v][0], dp[v][1]);
        dp[u][1] += dp[v][0];
    }
}
// answer = max(dp[root][0], dp[root][1])
```

## 10. DP with Bitmask – Travelling Salesman Problem (TSP)

**Problem**: Shortest path visiting all cities exactly once and returning to start.

**DP State**: `dp[mask][i]` = minimum distance to have visited set `mask` ending at city `i`.

```cpp
int tsp(vector<vector<int>>& dist) {
    int n = dist.size();
    int FULL = (1 << n) - 1;
    vector<vector<int>> dp(1 << n, vector<int>(n, INT_MAX/2));
    dp[1][0] = 0; // start at city 0
    for (int mask = 1; mask < (1 << n); ++mask) {
        for (int i = 0; i < n; ++i) {
            if (!(mask & (1 << i)) || dp[mask][i] >= INT_MAX/2) continue;
            for (int j = 0; j < n; ++j) {
                if (mask & (1 << j)) continue;
                dp[mask | (1 << j)][j] = min(dp[mask | (1 << j)][j], dp[mask][i] + dist[i][j]);
            }
        }
    }
    int ans = INT_MAX;
    for (int i = 0; i < n; ++i)
        ans = min(ans, dp[FULL][i] + dist[i][0]);
    return ans;
}
```

**Time**: O(2^n * n²). **Space**: O(2^n * n).  
**Real‑life analogy**: Delivery route planning – which order to visit customers to minimise travel.

## 11. Kadane’s Algorithm (DP view)

Kadane’s algorithm is a 1D DP for maximum subarray sum.

**DP Relation**: `dp[i] = max(nums[i], dp[i-1] + nums[i])` where `dp[i]` is max sum of subarray ending at i.

```cpp
int maxSubarraySum(vector<int>& nums) {
    int maxEndingHere = nums[0], maxSoFar = nums[0];
    for (int i = 1; i < nums.size(); ++i) {
        maxEndingHere = max(nums[i], maxEndingHere + nums[i]);
        maxSoFar = max(maxSoFar, maxEndingHere);
    }
    return maxSoFar;
}
```

## 12. Summary Table

| Problem Category | Classic Problem | Recurrence / Approach | Time Complexity |
|------------------|----------------|------------------------|------------------|
| 1D DP | Climbing Stairs | dp[i] = dp[i-1] + dp[i-2] | O(n) |
| 2D Grid | Min Path Sum | dp[i][j] = min(dp[i-1][j], dp[i][j-1]) + grid[i][j] | O(mn) |
| Subsequence | LCS | match => +1 else max(prev) | O(mn) |
| Subsequence | LIS | dp[i] = max(dp[j])+1 over j<i | O(n²) or O(n log n) |
| Edit Distance | Levenshtein | 1 + min(insert, delete, replace) | O(mn) |
| Knapsack | 0/1 Knapsack | dp[w] = max(dp[w], dp[w-wt]+val) | O(nW) |
| String | Wildcard Matching | dp[i][j] based on star handling | O(mn) |
| Tree DP | Max Independent Set | node selected/unselected | O(V+E) |
| Bitmask DP | TSP | dp[mask][i] = min over j | O(2ⁿ n²) |
| 1D DP | Kadane | maxEndingHere = max(x, cur+x) | O(n) |

The next chapter will cover advanced algorithmic techniques (greedy, divide and conquer, two pointers, and union‑find) and their applications.
