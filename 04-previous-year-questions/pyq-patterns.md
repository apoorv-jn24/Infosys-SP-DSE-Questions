# Previous-Year Question Patterns & Problem Bank

> [!IMPORTANT]
> Problem statements below are **paraphrased** based on real candidate reports. Infosys reuses *algorithmic patterns*, not verbatim text. Learn the pattern, practice the LeetCode analog, then solve the full problem in the numbered files.

---

## 20 Solved Problems — Quick Reference

| # | File | Tier | Topic | Key Technique | Online Trap? |
|---|---|---|---|---|---|
| 1 | [01-maximum-subarray-sum.md](01-maximum-subarray-sum.md) | Easy | Arrays | Kadane's Algorithm | — |
| 2 | [02-next-greater-element.md](02-next-greater-element.md) | Easy | Stack | Monotonic Stack | — |
| 3 | [03-rotate-array-by-k.md](03-rotate-array-by-k.md) | Easy | Arrays | Reversal Algorithm | — |
| 4 | [04-summer-array-min-swaps.md](04-summer-array-min-swaps.md) | Easy | Greedy | Inversion Count — **NOT bubble sort** | ⚠️ Yes |
| 5 | [05-min-base-identical-digits.md](05-min-base-identical-digits.md) | Easy | Number Theory | Base Search + 2-Digit Divisor Scan | ⚠️ Yes |
| 6 | [06-monster-quest.md](06-monster-quest.md) | Medium | Greedy | Sort + Exchange Argument | — |
| 7 | [07-andys-vacation.md](07-andys-vacation.md) | Medium | Greedy | Streak Counting | — |
| 8 | [08-min-ugliness-binary-string.md](08-min-ugliness-binary-string.md) | Medium | Greedy | Regret Heap on Non-adjacent Runs | ⚠️ Yes |
| 9 | [09-trapping-rain-water.md](09-trapping-rain-water.md) | Medium | Two Pointers | Prefix-Max / Two Pointers | — |
| 10 | [10-number-of-islands.md](10-number-of-islands.md) | Medium | Graphs | BFS / DFS on Grid | — |
| 11 | [11-coin-change.md](11-coin-change.md) | Medium | DP | Unbounded Knapsack DP | — |
| 12 | [12-max-xor-sum-in-range.md](12-max-xor-sum-in-range.md) | Medium | Bit Manipulation | Linear XOR Basis + Gauss-Jordan RREF | ⚠️ Yes |
| 13 | [13-longest-common-subsequence.md](13-longest-common-subsequence.md) | Hard | DP | 2D DP (LCS) | — |
| 14 | [14-counting-divisible-arrays.md](14-counting-divisible-arrays.md) | Hard | Number Theory | CRT + Polynomial Exponentiation | ⚠️ Yes |
| 15 | [15-packing-gifts-into-k-boxes.md](15-packing-gifts-into-k-boxes.md) | Hard | Greedy | Binary Search on Answer ($O(N \log \Sigma)$) | ⚠️ Yes |
| 16 | [16-longest-increasing-path-matrix.md](16-longest-increasing-path-matrix.md) | Hard | DFS + Memo | Topological DFS on Grid | — |
| 17 | [17-max-xor-half-sized-subset.md](17-max-xor-half-sized-subset.md) | Hard | Bit Manipulation | Gaussian Elimination over GF(2) | — |
| 18 | [18-longest-bitwise-compatible-lis.md](18-longest-bitwise-compatible-lis.md) | Hard | Bit Manip + LIS | **MSB-index LIS** — not plain value LIS | ⚠️ Yes |
| 19 | [19-largest-set-product-1-mod-n.md](19-largest-set-product-1-mod-n.md) | Hard | Number Theory | **Euler's Totient + Primitive Root Parity** | ⚠️ Yes |
| 20 | [20-balls-and-buckets-probability.md](20-balls-and-buckets-probability.md) | Hard | Probability | Combinatorics / Convolution DP | — |

---

## Documented Online Errors & Corrections

> [!CAUTION]
> The following problems have **incorrect or incomplete solutions** widely circulated online. Using naive approaches will fail hidden test cases.

### Problem 4 — Summer Array: Min Swaps
- **Wrong online answer**: Simulates actual bubble sort swaps — $O(N^2)$. Times out for $N = 10^5$.
- **Correct approach**: Count inversions using Merge Sort or a Fenwick Tree in $O(N \log N)$. Number of adjacent swaps = number of inversions.

### Problem 5 — Minimum Base with Identical Digits
- **Wrong online answer**: Scans bases up to $\sqrt{N}$ and falls back to $N-1$, missing two-digit representations `"dd"` where $N = d(b+1)$ for $d > 1$.
- **Correct approach**: Scan divisors $d \leq \sqrt{N}$ where $d < N/d - 1$ to find the smallest valid base $b = N/d - 1$.

### Problem 8 — Minimum Ugliness of Binary String
- **Wrong online answer**: Applies a contiguous sliding window flip of length $K$, failing when arbitrary flips across the string are permitted.
- **Correct approach**: Compress string into runs and use regret-greedy optimization with a priority queue to select non-adjacent interior runs to flip.

### Problem 12 — Maximum XOR-Sum in Range [0, K]
- **Wrong online answer**: Uses upper-triangular XOR basis without clearing higher bits, causing lower-bit changes to exceed $K$.
- **Correct approach**: Convert basis to Reduced Row Echelon Form (RREF) via Gauss-Jordan elimination before greedy query.

### Problem 14 — Counting Divisible Arrays
- **Wrong online answer**: Uses prime inclusion-exclusion assuming prime multiplicity 1, failing when $N$ contains non-square-free prime powers (e.g. $N=4$).
- **Correct approach**: Factorize $N$ and compute generating function powers $(P(x)^K \bmod x^a)$ modulo each prime power via the Chinese Remainder Theorem.

### Problem 15 — Packing Gifts into K Boxes
- **Wrong online answer**: Sorts weights descending and uses greedy bin-packing, violating contiguous subarray order.
- **Correct approach**: Preserve given element sequence and binary search on capacity ($O(N \log(\sum w))$).

### Problem 18 — Longest Bitwise-Compatible LIS
- **Wrong online answer**: Runs standard LIS on raw values, ignoring the bitwise compatibility condition entirely.
- **Correct approach**: Decode "bitwise compatibility" as *strictly increasing MSB indices*. The LIS must be built on MSB positions, not raw values. Use $O(N \log N)$ patience sorting on MSB indices.

### Problem 19 — Largest Set with Product 1 mod N
- **Wrong online answer**: Computes $(N-1)!$ (overflowing 32-bit int) or assumes $\varphi(N)$ unconditionally.
- **Correct approach**: By Gauss's generalization of Wilson's theorem, the product of all coprime integers is $\equiv -1 \pmod N$ whenever $N$ has a primitive root ($N \in \{2, 4, p^k, 2p^k\}$). For such $N > 2$, drop element $N-1 \equiv -1$ to get size $\varphi(N) - 1$.

---

## Pattern Catalog (19 Core Patterns)

*This extends the solved problems with broader pattern recognition for unseen questions.*

### Easy Patterns

**Pattern E1 — Consecutive Subarray / Streak Counting**
- Shape: Max length contiguous sequence satisfying a condition (at most $K$ absences, non-decreasing streak).
- Technique: Single-pass counter, Kadane's variation.
- Complexity: $O(N)$ time, $O(1)$ space.
- LeetCode: 485 (Max Consecutive Ones), 1446 (Consecutive Characters).

**Pattern E2 — Frequency-Based Filtering**
- Shape: Delete elements with frequency $> K$, or find first element matching a frequency parity condition.
- Technique: Hash map frequency count (2-pass).
- Complexity: $O(N)$ time, $O(U)$ space.
- LeetCode: 387 (First Unique Character), 1370 (Increasing Decreasing String).

**Pattern E3 — Matrix Traversal & Layer Manipulation**
- Shape: Spiral/diagonal traversal, rotate concentric layers by $K$ positions.
- Technique: 4 boundary pointers (`top`, `bottom`, `left`, `right`), simulation.
- Complexity: $O(N \times M)$ time, $O(1)$ extra space.
- LeetCode: 54 (Spiral Matrix), 48 (Rotate Image).

**Pattern E4 — Two-Pointer Partitioning**
- Shape: Rearrange array so negatives/evens appear before positives/odds.
- Technique: Read/write pointer (stable) or converging pointers (unstable).
- LeetCode: 283 (Move Zeroes), 905 (Sort Array By Parity).

---

### Medium Patterns

**Pattern M1 — Min Adjacent Swaps to Group Target Elements**
- Shape: Group all target elements together using minimum adjacent swaps.
- Technique: Collect target indices → find median → sum distances. **Do NOT simulate swaps.**
- Complexity: $O(N)$ time, $O(K)$ space.
- LeetCode: 1703 (Min Adjacent Swaps for K Consecutive Items).

**Pattern M2 — Interval Merging & Scheduling**
- Shape: Max non-overlapping jobs, or minimum servers for all jobs (Meeting Rooms II).
- Technique: Sort by end time (max schedule); Min-Heap of end times (min servers).
- Complexity: $O(N \log N)$ time.
- LeetCode: 435 (Non-overlapping Intervals), 253 (Meeting Rooms II).

**Pattern M3 — Variable-Length Sliding Window**
- Shape: Longest subarray/substring with at most $K$ distinct elements or sum $\leq S$.
- Technique: Hash map for window frequency; expand right, shrink left on violation.
- Complexity: $O(N)$ time.
- LeetCode: 904 (Fruit Into Baskets), LC3 (Longest Substring Without Repeating Characters).

**Pattern M4 — Heap / Priority Queue Top-K**
- Shape: K-th largest score in stream; minimize max sum when pairing elements.
- Technique: Min-Heap of size $K$; pop when size exceeds $K$.
- Complexity: $O(N \log K)$.
- LeetCode: 215 (Kth Largest Element), 347 (Top K Frequent Elements).

**Pattern M5 — Tree Path Sum**
- Shape: Max path sum between any two nodes (not necessarily root); count paths summing to target.
- Technique: Post-order DFS; propagate max branch sum upward.
- Complexity: $O(N)$ time, $O(H)$ space.
- LeetCode: 124 (Binary Tree Max Path Sum), 437 (Path Sum III).

---

### Hard Patterns

**Pattern H1 — Grid DP (Minimum Cost Path)**
- Shape: Start at $(0,0)$, reach $(N-1, M-1)$, move right/down, find minimum cost.
- State: `dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])`.
- Complexity: $O(N \times M)$ time, $O(M)$ space with 1D buffer.
- LeetCode: 64 (Min Path Sum), 63 (Unique Paths II).

**Pattern H2 — 0/1 Knapsack / Subset Sum**
- Shape: Max value selecting items with weight $\leq W$; partition array into two equal-sum subsets.
- State: `dp[w] = max(dp[w], dp[w - weight[i]] + value[i])`.
- Complexity: $O(N \times W)$ time, $O(W)$ space.
- LeetCode: 416 (Partition Equal Subset Sum), 474 (Ones and Zeroes).

**Pattern H3 — Modified Dijkstra (Multi-Constraint)**
- Shape: Min cost path from $S$ to $D$ with total travel time $\leq T_{max}$.
- State: `dist[node][time]`; push `(cost, node, time)` into min-heap.
- Complexity: $O(E \cdot T \log(V \cdot T))$.
- LeetCode: 787 (Cheapest Flights Within K Stops), 1928 (Min Cost to Reach Destination in Time).

**Pattern H4 — LIS in $O(N \log N)$**
- Shape: Length of longest strictly increasing subsequence; max weighted increasing subsequence.
- Technique: Patience sorting — `bisect_left` on `tails` array.
- Complexity: $O(N \log N)$ time.
- LeetCode: 300 (LIS), 354 (Russian Doll Envelopes).

**Pattern H5 — DSU / Connected Components**
- Shape: Min cable re-connections to unify all computers into one network.
- Technique: DSU with path compression + rank; count redundant edges and isolated components.
- Complexity: $O(E \cdot \alpha(V))$.
- LeetCode: 1319 (Network Connected), 684 (Redundant Connection).

**Pattern H6 — Modular Arithmetic & Number Theory**
- Shape: $(A^B) \bmod M$; count subsets with product $\equiv 1 \pmod M$.
- Technique: Binary exponentiation $O(\log B)$; apply modulo at every step.
- LeetCode: 50 (Pow(x,n)), GfG Modular Exponentiation.

**Pattern H7 — Bitmask / XOR Subset**
- Shape: Choose subset of $N \leq 20$ numbers to maximize XOR; find max XOR of two numbers.
- Technique: Iterate all $2^N$ masks for small $N$; Trie-based XOR for large $N$.
- LeetCode: 421 (Max XOR of Two Numbers in Array), 1178 (Valid Words for Each Puzzle).

**Pattern H8 — Trie Prefix Query**
- Shape: Count words in dictionary starting with given prefix.
- Technique: Trie with `prefix_count` at every node; increment on insert, return on query.
- Complexity: $O(L)$ per operation.
- LeetCode: 208 (Implement Trie), 1804 (Implement Trie II).

---

### DSE-Specific Patterns

**Pattern D1 — String Tokenization & Log Parsing**
- Shape: Filter raw log strings (`TIMESTAMP|LEVEL|SERVICE|MESSAGE`) by service and level; sort chronologically.
- Technique: Split by delimiter, map to struct, sort by timestamp.
- LeetCode: 937 (Reorder Data in Log Files).

**Pattern D2 — LRU Cache Design**
- Shape: `get(key)` and `put(key, value)` in $O(1)$; evict Least Recently Used on capacity.
- Technique: Doubly Linked List + Hash Map.
- LeetCode: 146 (LRU Cache).
