# Chapter 12: Greedy Algorithms

Greedy algorithms build a solution step by step by always choosing the locally optimal choice (the one that looks best at the moment) without revisiting previous decisions. This chapter covers the greedy choice property, classic problems (activity selection, fractional knapsack, job sequencing, Huffman coding, coin change, minimum platforms), and comparisons with dynamic programming.

## 1. Greedy Choice Property

**What**: A problem exhibits the greedy choice property if a globally optimal solution can be reached by making a sequence of locally optimal (greedy) choices.

**Optimal substructure**: The problem can be broken down into subproblems, and the greedy choice combined with an optimal solution to the remaining subproblem yields an optimal solution for the original problem.

**When to use greedy**:
- The problem can be solved by a series of choices, each selecting the “best” available at that moment.
- The choice does not depend on future choices.
- Greedy choice property and optimal substructure both hold.

**When greedy fails**:
- Problems that require considering trade‑offs (e.g., 0/1 knapsack, longest path).
- Problems with overlapping subproblems that benefit from DP (e.g., edit distance, shortest path with negative edges).

**Real‑life analogy**: Getting change with the fewest coins using standard denominations (quarters, dimes, nickels, pennies) – always pick the largest coin that fits. This greedy works for US coins but fails for arbitrary denominations (e.g., coins 1, 3, 4 – target 6: greedy picks 4+1+1=3 coins, but optimal is 3+3=2 coins).

## 2. Activity Selection

**Problem**: Given n activities with start and finish times, select the maximum number of non‑overlapping activities.

**Greedy choice**: Always pick the activity that finishes earliest. This leaves the most remaining time for other activities.

**Algorithm**:
1. Sort activities by finish time.
2. Pick the first activity.
3. For each subsequent activity, if its start time ≥ last chosen finish time, select it.

```cpp
struct Activity { int start, finish; };
bool compare(Activity a, Activity b) { return a.finish < b.finish; }

int activitySelection(vector<Activity>& activities) {
    sort(activities.begin(), activities.end(), compare);
    int count = 1;
    int lastFinish = activities[0].finish;
    for (int i = 1; i < activities.size(); ++i) {
        if (activities[i].start >= lastFinish) {
            count++;
            lastFinish = activities[i].finish;
        }
    }
    return count;
}
```

**Time**: O(n log n) due to sorting. **Space**: O(1) extra.

**Real‑life analogy**: Scheduling the most meetings in a conference room – always choose the meeting that ends earliest, freeing the room for subsequent meetings.

## 3. Fractional Knapsack

**Problem**: Given items with weight and value, and a knapsack capacity, maximise total value by taking fractions of items (you can break items arbitrarily).

**Greedy choice**: Take items with the highest value per unit weight (value/weight ratio) first.

```cpp
struct Item { int value, weight; };
bool compare(Item a, Item b) { 
    return (double)a.value/a.weight > (double)b.value/b.weight; 
}

double fractionalKnapsack(vector<Item>& items, int capacity) {
    sort(items.begin(), items.end(), compare);
    double totalValue = 0.0;
    for (Item& item : items) {
        if (capacity >= item.weight) {
            totalValue += item.value;
            capacity -= item.weight;
        } else {
            totalValue += item.value * ((double)capacity / item.weight);
            break;
        }
    }
    return totalValue;
}
```

**Time**: O(n log n). **Space**: O(1).

**Why greedy works**: Because you can take fractions, filling the remaining capacity with the highest‑ratio item is always optimal. This differs from 0/1 knapsack, where greedy fails.

**Real‑life analogy**: You have a bag of limited size and want to carry the most valuable mixture of grains (e.g., gold dust, silver dust, copper dust). You take the most expensive dust first, possibly partially.

## 4. Job Sequencing with Deadlines

**Problem**: Each job has a deadline and a profit, takes unit time, and can be scheduled at most one job per time unit. Maximise total profit.

**Greedy choice**: Sort jobs by profit descending. For each job, schedule it at the latest available free slot before its deadline.

```cpp
struct Job { int id, deadline, profit; };
bool compare(Job a, Job b) { return a.profit > b.profit; }

int jobSequencing(vector<Job>& jobs) {
    sort(jobs.begin(), jobs.end(), compare);
    int maxDeadline = 0;
    for (auto& j : jobs) maxDeadline = max(maxDeadline, j.deadline);
    vector<int> slot(maxDeadline + 1, -1);
    int totalProfit = 0;
    for (Job& j : jobs) {
        for (int t = j.deadline; t > 0; --t) {
            if (slot[t] == -1) {
                slot[t] = j.id;
                totalProfit += j.profit;
                break;
            }
        }
    }
    return totalProfit;
}
```

**Time**: O(n²) worst case (can be improved to O(n log n) using disjoint set union). **Space**: O(maxDeadline).

**Real‑life analogy**: Freelancer accepting projects with deadlines and payments; you can only do one project per day, so you prioritise high‑paying jobs and schedule them as late as possible to leave room for other jobs.

## 5. Huffman Coding

**Problem**: Given character frequencies, build a prefix‑free binary code that minimises the total encoded length.

**Greedy choice**: Repeatedly merge the two nodes with smallest frequencies.

**Algorithm**:
1. Create a leaf node for each character with its frequency.
2. Insert all nodes into a min‑heap.
3. While heap has more than one node:
   - Extract two minimum frequency nodes.
   - Create a new internal node with frequency = sum of the two.
   - Make the two nodes its children.
   - Insert the new node into the heap.
4. The remaining node is the root of the Huffman tree.

```cpp
struct HuffmanNode {
    char ch;
    int freq;
    HuffmanNode *left, *right;
    HuffmanNode(char c, int f) : ch(c), freq(f), left(nullptr), right(nullptr) {}
    HuffmanNode(int f, HuffmanNode* l, HuffmanNode* r) : ch('\0'), freq(f), left(l), right(r) {}
};
struct Compare {
    bool operator()(HuffmanNode* a, HuffmanNode* b) { return a->freq > b->freq; }
};

HuffmanNode* buildHuffmanTree(vector<pair<char, int>>& freqTable) {
    priority_queue<HuffmanNode*, vector<HuffmanNode*>, Compare> pq;
    for (auto& p : freqTable)
        pq.push(new HuffmanNode(p.first, p.second));
    while (pq.size() > 1) {
        HuffmanNode* left = pq.top(); pq.pop();
        HuffmanNode* right = pq.top(); pq.pop();
        HuffmanNode* parent = new HuffmanNode(left->freq + right->freq, left, right);
        pq.push(parent);
    }
    return pq.top();
}
// Then traverse the tree to generate codes.
```

**Time**: O(n log n) (n = number of unique characters). **Space**: O(n).

**Real‑life analogy**: Assigning shorter codes to common letters in Morse code (e.g., 'E' is '.') to minimise overall message length.

## 6. Coin Change (Greedy vs DP)

**Problem**: Find the minimum number of coins to make a given amount, given coin denominations.

**Greedy approach**: Always pick the largest coin that does not exceed the remaining amount.

**When greedy works**: When the coin system is *canonical* (e.g., US coins: 1,5,10,25). Example: amount = 30, coins [1,5,10,25] – greedy picks 25+5 = 2 coins.

**When greedy fails**: Non‑canonical systems. Example: coins = [1,3,4], amount = 6. Greedy picks 4+1+1 = 3 coins, but optimal is 3+3 = 2 coins. For such cases, use DP.

**DP solution (minimum coins)**:

```cpp
int coinChangeDP(vector<int>& coins, int amount) {
    vector<int> dp(amount+1, amount+1);
    dp[0] = 0;
    for (int i = 1; i <= amount; ++i)
        for (int c : coins)
            if (c <= i)
                dp[i] = min(dp[i], dp[i-c] + 1);
    return dp[amount] > amount ? -1 : dp[amount];
}
```

**Takeaway**: Use greedy only if the coin system is proven canonical; otherwise use DP for exact minimum.

## 7. Minimum Number of Platforms (Interval Scheduling)

**Problem**: Given arrival and departure times of trains, find the minimum number of platforms needed so that no train waits.

**Greedy approach**: Sort arrivals and departures separately. Use two pointers to simulate platform usage, counting overlapping intervals.

```cpp
int findPlatform(vector<int>& arr, vector<int>& dep) {
    sort(arr.begin(), arr.end());
    sort(dep.begin(), dep.end());
    int platforms = 0, maxPlatforms = 0;
    int i = 0, j = 0;
    int n = arr.size();
    while (i < n && j < n) {
        if (arr[i] <= dep[j]) {
            platforms++;
            i++;
            maxPlatforms = max(maxPlatforms, platforms);
        } else {
            platforms--;
            j++;
        }
    }
    return maxPlatforms;
}
```

**Time**: O(n log n). **Space**: O(1).

**Real‑life analogy**: A railway station where you need to determine the peak number of simultaneous trains.

## 8. When NOT to Use Greedy

| Problem | Why Greedy Fails | Better Approach |
|---------|------------------|-----------------|
| 0/1 Knapsack | Taking highest value/weight may leave capacity that cannot be filled fractionally | DP |
| Longest Path in DAG (unweighted) | Greedy (take edge to next node with many outgoing) does not guarantee longest | DP on DAG or BFS with modifications |
| Coin change (arbitrary denominations) | Greedy may pick large coin that prevents optimal combination | DP |
| Minimum cost to reach end with variable jumps | Not every locally shortest jump leads to global optimum | DP or Dijkstra |

## 9. Summary Table

| Problem | Greedy Choice | Time Complexity | Notes |
|---------|---------------|-----------------|-------|
| Activity Selection | Earliest finish time | O(n log n) | Optimal for non‑weighted intervals |
| Fractional Knapsack | Highest value/weight | O(n log n) | Allows fractions |
| Job Sequencing | Highest profit, schedule as late as possible | O(n²) or O(n log n) with DSU | Unit time jobs |
| Huffman Coding | Merge smallest frequencies | O(n log n) | Produces optimal prefix code |
| Coin Change (canonical) | Largest coin ≤ remaining | O(n log n) if sorted | Fails for non‑canonical |
| Minimum Platforms | Sweep line over sorted times | O(n log n) | Counts maximum overlaps |

The next chapter will cover advanced topics: divide and conquer (master theorem, closest pair, Strassen’s matrix multiplication) and algorithmic paradigms.
