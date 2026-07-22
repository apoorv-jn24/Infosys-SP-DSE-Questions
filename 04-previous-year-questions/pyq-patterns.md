# Previous-Year Question Patterns & Real Exam Question Bank

> [!IMPORTANT]
> **Important Compliance Note**: The problem patterns below are **paraphrased approach guides and pattern analyses** based on real candidate experiences and reported exam slots from recent Infosys SP/DSE drives. They are NOT copy-pasted problem statements. Infosys reuses *underlying algorithmic patterns and problem shapes*, not verbatim question text. Learn the pattern, understand the optimal technique, and practice the corresponding LeetCode/GfG problem types.

---

## Easy-Tier Patterns (Q1-Style Questions)

### Pattern 1 — Consecutive Subarray / Streak-Counting Framing
- **Real Exam Problem Shape**: Given a string or array representing daily status (e.g., student attendance `'P'`/`'A'`, stock upward/downward movement, or color sequence of berries), find the maximum length of a contiguous sequence satisfying a given rule (e.g., at most $K$ consecutive absences or maximum streak of non-decreasing values).
- **Underlying Skill**: Single-pass traversal, sliding window with a counter, Kadane's variation.
- **Approach Note**: Keep a running streak count `current_streak` and update `max_streak` whenever the condition holds. Reset or decrement counters cleanly when encountering invalid elements.
- **Complexity Goal**: $O(N)$ time, $O(1)$ space.
- **Practice Problems**: LeetCode 485 (Max Consecutive Ones), LeetCode 1446 (Consecutive Characters).

### Pattern 2 — Frequency-Based Character / Element Filtering
- **Real Exam Problem Shape**: Given an array of integers or a string of characters, transform it by deleting elements that appear with a frequency greater than $K$, or find the first element whose frequency meets a specific parity condition.
- **Underlying Skill**: Hash map / Frequency array lookup, two-pass iteration.
- **Approach Note**: Pass 1: Build a frequency map using a hash map or fixed-size array (`int freq[26]` / `int freq[256]`). Pass 2: Filter or construct the result array based on the map.
- **Complexity Goal**: $O(N)$ time, $O(U)$ space where $U$ is number of unique keys.
- **Practice Problems**: LeetCode 387 (First Unique Character in a String), LeetCode 1370 (Increasing Decreasing String).

### Pattern 3 — Matrix Traversal & Layer Manipulation
- **Real Exam Problem Shape**: Given an $N \times M$ matrix, traverse it in spiral order or diagonal order, or rotate specific concentric layers by $K$ positions.
- **Underlying Skill**: Boundary manipulation (`top`, `bottom`, `left`, `right` pointers), simulation.
- **Approach Note**: Maintain 4 boundary variables and shrink them after each directional pass (left-to-right, top-to-bottom, right-to-left, bottom-to-top).
- **Complexity Goal**: $O(N \times M)$ time, $O(1)$ extra space.
- **Practice Problems**: LeetCode 54 (Spiral Matrix), LeetCode 48 (Rotate Image).

### Pattern 4 — Two-Pointer In-Place Filtering & Partitioning
- **Real Exam Problem Shape**: Rearrange an array so that all negative numbers or even numbers appear before positive/odd numbers, preserving their original relative order if possible.
- **Underlying Skill**: Two pointers (Read/Write pointer), Stable Partitioning.
- **Approach Note**: If relative order doesn't matter, use left/right converging pointers. If relative order matters (stable), use a write pointer or temporary auxiliary array.
- **Complexity Goal**: $O(N)$ time, $O(1)$ or $O(N)$ space.
- **Practice Problems**: LeetCode 283 (Move Zeroes), LeetCode 905 (Sort Array By Parity).

---

## Medium-Tier Patterns (Q2-Style Questions)

### Pattern 5 — "Rearrange Array / String with Minimum Adjacent Swaps"
- **Real Exam Problem Shape**: Given a binary array or string of characters, rearrange it so all target elements (e.g., all `1`s or all vowels) end up adjacent to each other using the *minimum number of adjacent swaps*.
- **Underlying Skill**: Greedy counting, Two pointers / Median index placement.
- **Approach Note**: Do NOT simulate actual swaps! Collect the indices of all target elements into a list `pos`. The optimal meeting point for all target elements is the median element in `pos`. The total minimum swaps is the sum of distances from each target element to its final compact position around the median.
- **Complexity Goal**: $O(N)$ time, $O(K)$ space where $K$ is number of target elements.
- **Practice Problems**: LeetCode 1703 (Minimum Adjacent Swaps for K Consecutive Items), LeetCode 1151 (Minimum Swaps to Group All 1's Together).

### Pattern 6 — Interval Merging & Scheduling Optimization
- **Real Exam Problem Shape**: Given a set of time intervals `[start, end]` representing events, servers, or job processing windows, find the maximum number of non-overlapping jobs that can be scheduled, or the minimum number of servers needed to process all jobs.
- **Underlying Skill**: Greedy algorithms, Sorting by end time vs. start time, Priority Queues.
- **Approach Note**: To maximize non-overlapping jobs: Sort intervals by `end_time` ascending. Iterate and pick the next job whose `start_time` $\ge$ last selected job's `end_time`. To find minimum servers (Meeting Rooms II): Sort start times and end times separately or use a Min-Heap of end times.
- **Complexity Goal**: $O(N \log N)$ time, $O(N)$ space.
- **Practice Problems**: LeetCode 435 (Non-overlapping Intervals), LeetCode 253 (Meeting Rooms II), LeetCode 56 (Merge Intervals).

### Pattern 7 — Sliding Window with Fixed / Dynamic Constraint
- **Real Exam Problem Shape**: Given an array of numbers or characters, find the longest contiguous subarray/substring containing at most $K$ distinct elements, or whose sum is $\le S$.
- **Underlying Skill**: Sliding Window (Expand right pointer, contract left pointer when constraint is violated).
- **Approach Note**: Use a Hash Map to store frequency of elements inside window `[left...right]`. Expand `right`. If `map.size() > K`, shrink `left` until `map.size() <= K`. Record `max_length = max(max_length, right - left + 1)`.
- **Complexity Goal**: $O(N)$ time, $O(K)$ space.
- **Practice Problems**: LeetCode 904 (Fruit Into Baskets / Longest Subarray with at most 2 distinct), LeetCode 3 (Longest Substring Without Repeating Characters).

### Pattern 8 — Heap / Priority Queue Top-K Optimization
- **Real Exam Problem Shape**: You are given $N$ streams or tasks with scores/frequencies and need to continuously extract the $K$-th largest score or minimize the maximum sum when pairing elements.
- **Underlying Skill**: Min-Heap / Max-Heap (`std::priority_queue` in C++, `heapq` in Python, `PriorityQueue` in Java).
- **Approach Note**: To keep track of Top-$K$ elements in an $N$-element stream, use a **Min-Heap** of max size $K$. Push element; if heap size $> K$, pop top. The top of the Min-Heap is always the $K$-th largest element!
- **Complexity Goal**: $O(N \log K)$ time, $O(K)$ space.
- **Practice Problems**: LeetCode 215 (Kth Largest Element in an Array), LeetCode 347 (Top K Frequent Elements).

### Pattern 9 — Tree Path Constraint / Boundary Calculation
- **Real Exam Problem Shape**: Given a binary tree with node values, find the maximum path sum between any two nodes (not necessarily passing through the root), or count paths that sum to a target value.
- **Underlying Skill**: Tree DFS / Recursion with bottom-up state propagation.
- **Approach Note**: For each node `curr`, recursively calculate maximum left branch sum `L` and right branch sum `R` (ignoring negative sums). The maximum path *passing through `curr`* is `curr.val + L + R`. Update global maximum. Return `curr.val + max(L, R)` to parent.
- **Complexity Goal**: $O(N)$ time, $O(H)$ recursion stack space.
- **Practice Problems**: LeetCode 124 (Binary Tree Maximum Path Sum), LeetCode 437 (Path Sum III).

---

## Hard-Tier Patterns (Q3-Style Questions — SP / High-Score DSE)

### Pattern 10 — Dynamic Programming: Grid Path & Minimum Cost Walk
- **Real Exam Problem Shape**: Given an $N \times M$ grid filled with cost values, start at `(0,0)` and reach `(N-1, M-1)`. You can only move Right or Down (or down-left/down-right). Some cells may be blocked or contain special multipliers. Find the minimum total cost path.
- **Underlying Skill**: 2D Dynamic Programming (Tabulation / Top-Down Memoization).
- **Approach Note**:
  - State: `dp[i][j]` = Minimum cost to reach cell `(i, j)`.
  - Recurrence: `dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])`.
  - Base Cases: `dp[0][0] = grid[0][0]`, initialize first row and first column cumulatively.
  - Handle obstacles: If `grid[i][j] == BLOCKED`, `dp[i][j] = INF`.
- **Complexity Goal**: $O(N \times M)$ time, $O(M)$ space with 1D row buffer.
- **Practice Problems**: LeetCode 64 (Minimum Path Sum), LeetCode 63 (Unique Paths II).

### Pattern 11 — Dynamic Programming: Subsequence / Knapsack Optimization
- **Real Exam Problem Shape**: You are given $N$ items with values and weights (or an array of integers). Find the maximum score by choosing a subset such that total weight $\le W$, or determine if the array can be partitioned into two subsets with equal sum.
- **Underlying Skill**: 0/1 Knapsack DP, Subset Sum DP.
- **Approach Note**:
  - State: `dp[w]` = Maximum value attainable with weight budget `w`.
  - Outer loop over items `1..N`, inner loop over weight `W` down to `weight[i]`.
  - Recurrence: `dp[w] = max(dp[w], dp[w - weight[i]] + value[i])`.
- **Complexity Goal**: $O(N \times W)$ time, $O(W)$ space.
- **Practice Problems**: LeetCode 416 (Partition Equal Subset Sum), LeetCode 474 (Ones and Zeroes).

### Pattern 12 — Graph: Shortest Path with Modified Constraints (Dijkstra Variant)
- **Real Exam Problem Shape**: Given a weighted graph of $N$ cities connected by roads with toll costs and travel times, find the minimum toll cost path from source $S$ to destination $D$ such that total travel time does NOT exceed $T$ max hours.
- **Underlying Skill**: Modified Dijkstra algorithm using Priority Queue storing `(current_cost, current_node, current_time)`.
- **Approach Note**: Use a 2D distance state `dist[node][time]` representing minimum cost to reach `node` with elapsed time `time`. Push `(0, source, 0)` into Min-Heap. When popping `(cost, u, t)`, iterate neighbors `v` with edge `(u, v, toll, time_needed)`. If `t + time_needed <= T` and new cost is better than `dist[v][t + time_needed]`, update and push.
- **Complexity Goal**: $O(E \cdot T \log(V \cdot T))$ time, $O(V \cdot T)$ space.
- **Practice Problems**: LeetCode 787 (Cheapest Flights Within K Stops), LeetCode 1928 (Minimum Cost to Reach Destination in Time).

### Pattern 13 — Dynamic Programming: Longest Increasing Subsequence (LIS) & Variants
- **Real Exam Problem Shape**: Given an array of integers, find the length of the longest subsequence such that elements are strictly increasing, or find the maximum weighted sum of an increasing subsequence.
- **Underlying Skill**: LIS via $O(N \log N)$ Binary Search / Patient Sorting (`std::lower_bound`).
- **Approach Note**: Maintain an array `tails` where `tails[i]` stores the smallest tail of all increasing subsequences of length `i+1`. For each element `x` in input: If `x` is larger than all elements in `tails`, append `x`. Otherwise, replace the first element in `tails` that is $\ge x$ using binary search.
- **Complexity Goal**: $O(N \log N)$ time, $O(N)$ space.
- **Practice Problems**: LeetCode 300 (Longest Increasing Subsequence), LeetCode 354 (Russian Doll Envelopes).

### Pattern 14 — Graph: Connected Components & Redundant Connections (DSU)
- **Real Exam Problem Shape**: Given $N$ computers connected by network cables, find the minimum number of cable extractions and re-connections needed to connect all computers into a single unified network.
- **Underlying Skill**: Disjoint Set Union (DSU) with Path Compression & Rank.
- **Approach Note**: Count total extra redundant edges (`find(u) == find(v)` during initial graph building). Count number of isolated connected components `C`. To connect `C` components, we need `C - 1` free edges. If `redundant_edges >= C - 1`, return `C - 1`; else return `-1`.
- **Complexity Goal**: $O(E \cdot \alpha(V))$ time, $O(V)$ space.
- **Practice Problems**: LeetCode 1319 (Number of Operations to Make Network Connected), LeetCode 684 (Redundant Connection).

### Pattern 15 — Modular Arithmetic & Number Theory Framing
- **Real Exam Problem Shape**: You are given a large number $N$ and asked to compute the number of subsets whose product modulo $M$ equals 1, or find $(A^B) \pmod{10^9+7}$.
- **Underlying Skill**: Modular Exponentiation, Fermat's Little Theorem, DP over Modulo states.
- **Approach Note**: Always apply modulo at every addition and multiplication step: `(a + b) % M` and `(a * b) % M`. For exponentiation $A^B \pmod M$, use Binary Exponentiation ($O(\log B)$).
- **Complexity Goal**: $O(\log B)$ or $O(N \times M)$ DP.
- **Practice Problems**: LeetCode 50 (Pow(x, n)), GfG Modular Exponentiation problems.

### Pattern 16 — Bit Manipulation & Bitmasking for Subsets
- **Real Exam Problem Shape**: Given an array of $N$ numbers ($N \le 20$), choose a subset to maximize the total Bitwise XOR value, or find the maximum subset sum that satisfies bitwise constraints.
- **Underlying Skill**: Bitmask iteration (`1 << N`) or Trie-based XOR Maximization.
- **Approach Note**: For $N \le 20$, iterate all $2^N$ masks: `for mask in range(1 << N)`. For larger $N$, insert binary representations of numbers into a Trie and query for maximum opposite bits.
- **Complexity Goal**: $O(2^N)$ for small $N$, $O(N \log(\max A))$ for Trie approach.
- **Practice Problems**: LeetCode 421 (Maximum XOR of Two Numbers in an Array), LeetCode 1178 (Number of Valid Words for Each Puzzle).

### Pattern 17 — Trie-Based Prefix Query & Word Search
- **Real Exam Problem Shape**: Given a dictionary of words and a stream of prefix search queries, efficiently count how many words in the dictionary start with a given prefix.
- **Underlying Skill**: Trie (Prefix Tree) with `prefix_count` stored at each node.
- **Approach Note**: Each node has `children[26]` and `prefix_count`. When inserting a word, increment `prefix_count` on every node along the path. For query prefix `P`, traverse down `P` and return `node.prefix_count`.
- **Complexity Goal**: $O(L)$ per insert/query where $L$ is word length.
- **Practice Problems**: LeetCode 208 (Implement Trie), LeetCode 1804 (Implement Trie II).

---

## DSE-Specific Application & Implementation Patterns

### Pattern 18 — String Tokenization & Rule-Based Parsing (API/Log Filter)
- **Real Exam Problem Shape**: Given raw log strings formatted as `"TIMESTAMP|LEVEL|SERVICE|MESSAGE"`, parse and filter logs for a target `SERVICE` and `LEVEL`, sorting results chronologically.
- **Underlying Skill**: String splitting, struct/class mapping, custom sorting comparators.
- **Approach Note**: Split by delimiter `|`. Map each record to a structured object. Filter using lambda functions, then sort by timestamp string/epoch.
- **Complexity Goal**: $O(N \log N)$ time, $O(N)$ space.
- **Practice Problems**: LeetCode 593 (Valid Square / String Parsing), LeetCode 937 (Reorder Data in Log Files).

### Pattern 19 — Custom Cache Design (LRU / LFU Simulation)
- **Real Exam Problem Shape**: Design a data structure for a digital application cache that supports `get(key)` and `put(key, value)` in $O(1)$ average time, evicting the Least Recently Used (LRU) item when capacity is reached.
- **Underlying Skill**: Doubly Linked List + Hash Map (`unordered_map<int, list<pair<int,int>>::iterator>`).
- **Approach Note**: Hash Map provides $O(1)$ key lookup. Doubly Linked List maintains usage order. On `get`/`put`, move node to head of list. On eviction, remove node from tail of list and erase from map.
- **Complexity Goal**: $O(1)$ time for both `get` and `put`.
- **Practice Problems**: LeetCode 146 (LRU Cache).
