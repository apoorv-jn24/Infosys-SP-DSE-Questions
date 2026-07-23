# Coding Round — Topic Checklist

## 4-Week Study Plan

| Week | Daily Target | Topics | Problems |
|---|---|---|---|
| **Week 1** | 2–3 hrs/day | Arrays, Strings, Stacks, Queues, Hash Maps, Linked Lists | Problems 1–5 (Easy Tier) |
| **Week 2** | 3 hrs/day | Greedy, Sliding Window, Two Pointers, Trees, Heaps, Recursion | Problems 6–12 (Medium Tier) |
| **Week 3** | 3–4 hrs/day | Dynamic Programming, Graphs (BFS/DFS), DSU, Bit Manipulation, Number Theory | Problems 13–20 (Hard Tier) |
| **Week 4** | 2–3 hrs/day | Mock rounds, edge-case review, interview prep, re-solve trap problems (4, 15, 18, 19) | Full `05-interview-prep` |

---

## Non-Negotiable Prerequisites

Master these primitives before attempting Medium/Hard problems — they appear repeatedly across the 20 solved problems:

| Primitive | Why it matters | Quick reference |
|---|---|---|
| **XOR properties** | `a ^ a = 0`, `a ^ 0 = a`, XOR is commutative/associative | Problems 12, 17, 18 |
| **MSB (Most Significant Bit)** | `msb(x) = x.bit_length() - 1` in Python; `__lg(x)` in C++ | Problems 17, 18 |
| **Euler's Totient φ(N)** | Count integers in $[1, N]$ coprime to $N$; use $O(\sqrt{N})$ factorization | Problem 19 |
| **Inversion counting** | Count swaps to sort = number of inversions; $O(N \log N)$ via merge sort or BIT | Problem 4 |
| **Patience Sorting / LIS in $O(N \log N)$** | `bisect_left` on `tails` array; not $O(N^2)$ DP | Problems 13, 18 |
| **Harmonic divisor loops** | Sum over all $d \leq N$ of $\lfloor N/d \rfloor$ = $O(N \log N)$ — do not use nested loops | Problem 14 |

---

## Easy Tier (Q1 — 20 Marks)

Focus: correctness, edge-case safety, $O(N)$ or $O(N \log N)$ time.

- [ ] **Arrays** — traversal, in-place rotation, prefix sums, two-pointer basics, sliding window basics
  - *Practice*: Max sum subarray of size $K$ (Sliding Window)
  - *Practice*: Rotate array of $N$ elements right by $K$ steps in $O(1)$ space
  - *Evaluator check*: $O(N)$ time, $O(1)$ auxiliary space; handle $K > N$

- [ ] **Strings** — palindrome, anagram, string reversal, pattern matching basics
  - *Practice*: First non-repeating character in a string (single pass)
  - *Practice*: Determine if two strings are anagrams

- [ ] **Stacks & Queues** — balanced parentheses, next-greater-element, basic simulation
  - *Practice*: Valid parentheses check `()[]{}`, Min-Stack with $O(1)$ `getMin()`
  - *Evaluator check*: Avoid $O(N^2)$ brute-force for next-greater; use monotonic stack

- [ ] **Hash Maps & Sets** — frequency counting, two-sum lookups, intersection/union
  - *Practice*: Two-sum (target index lookup), majority element $> N/3$

- [ ] **Linked Lists** — reversal, cycle detection (Floyd's), merging sorted lists
  - *Practice*: Reverse singly linked list; detect cycle start node

- [ ] **Heaps / Priority Queue basics** — K-th largest, min-heap insertion/extraction
  - *Practice*: K-th largest in unsorted array using Min-Heap of size $K$ — $O(N \log K)$

---

## Medium Tier (Q2 — 30 Marks)

Focus: choosing the right technique, reducing from $O(N^2)$ to $O(N \log N)$ or $O(N)$.

- [ ] **Greedy Algorithms** — interval scheduling, minimum-swaps, exchange argument proofs
  - *Practice*: Activity selection (max non-overlapping); min adjacent swaps to group all 1s together
  - *Evaluator check*: Prove greedy choice property; sort by end time, not start time

- [ ] **Advanced Sliding Window & Two Pointers** — variable-length window, 3-Sum
  - *Practice*: Longest substring without repeating characters; all unique triplets summing to zero
  - *Evaluator check*: Handle window-shrink condition cleanly to avoid infinite loops

- [ ] **Monotonic Stack & Queue** — daily temperatures, sliding window maximum
  - *Practice*: Days until warmer temperature; largest rectangle in histogram

- [ ] **Recursion & Backtracking** — subset generation, permutations, combination sum
  - *Practice*: All combinations summing to target (elements reusable); N-Queens count
  - *Evaluator check*: Prune invalid branches early — no brute exponential recursion without pruning

- [ ] **Trees & BST** — BFS level-order, diameter, LCA
  - *Practice*: Diameter of binary tree; Lowest Common Ancestor (LCA)
  - *Evaluator check*: Handle skewed trees ($O(H)$ recursion stack space)

- [ ] **Greedy / DP Hybrid** — minimize/maximize operations (common Infosys phrasing)
  - *Practice*: Minimum operations to reduce number to 1 (subtract 1, divide by 2, divide by 3)

---

## Hard Tier (Q3 — 50 Marks)

Focus: recognizing subproblem overlap, DP state design, graph modeling, advanced patterns under time pressure.

- [ ] **Dynamic Programming (1D & 2D)** — Knapsack, LCS, LIS, Edit Distance, Grid Path Min Cost
  - *Practice*: Edit distance (insert/delete/replace); max profit with weight constraint; min cost grid path
  - *Evaluator check*: State definition must be precise; space-optimize $O(N \times M)$ to $O(M)$ where possible

- [ ] **Graph Algorithms** — BFS/DFS, Dijkstra, Topological Sort, Cycle Detection
  - *Practice*: Shortest path (Dijkstra); course scheduling validity (Topological Sort + cycle detection)
  - *Evaluator check*: Use adjacency lists for sparse graphs; maintain visited set

- [ ] **DSU (Disjoint Set Union / Union-Find)** — connected components, Kruskal's MST
  - *Practice*: Redundant connection in undirected graph
  - *Evaluator check*: Path compression + union by rank = $O(\alpha(N))$ per op

- [ ] **Bit Manipulation & Bitmask DP** — XOR subsets, counting set bits, bitmask state DP
  - *Practice*: Max XOR of two numbers in array; find two unique elements in array where all others appear twice
  - *Evaluator check*: Use `long long` / `long` when shifting > 31 bits

- [ ] **Number Theory** — modular exponentiation, GCD/LCM, Sieve, base conversion, Euler's totient
  - *Practice*: Compute $A^B \bmod C$ in $O(\log B)$; base-$K$ representation of $N$
  - *Evaluator check*: Safe modular subtraction: `(a % m + m) % m`

- [ ] **Advanced Data Structures (SP-tier)** — Trie, Segment Tree / Fenwick Tree
  - *Practice*: Implement Trie with `insert`, `search`, `startsWith`; range sum query with point updates

---

## Cross-Cutting Skills

Apply these throughout — not a separate section to study at the end:

- [ ] State Big-O time and space for every solution, unprompted
- [ ] Write edge-case-safe code: empty input, $N=1$, all-same elements, overflow-prone inputs
- [ ] Clean variable names and function decomposition — interviewers read code quality, not just pass rates

---

## DSE-Specific Additions

Layer these on top of the DSA checklist if targeting DSE specifically:

- [ ] **REST API basics** — write a GET/POST endpoint in your primary framework (FastAPI, Express, Spring Boot)
- [ ] **SQL** — joins, aggregations, subqueries, window functions → cross-reference with `05-interview-prep`
- [ ] **OOP fundamentals** — four pillars applied to a real design question, not just definitions
- [ ] **Git workflow** — describe your actual branch/merge/conflict-resolution workflow
- [ ] **System architecture** — client-server communication, JWT basics, SQL vs. NoSQL tradeoffs

---

## Last 48 Hours Strategy

| Priority | Action |
|---|---|
| 🔴 Critical | Re-solve Problems 4, 15, 18, 19 — these have widely-circulated wrong online solutions |
| 🟠 High | Run through all 5 high-cost mistakes in `02-syllabus-and-pattern` and verify you have fixes memorized |
| 🟡 Medium | Review your own weak topics from the checklist above |
| 🟢 Low | Skim `05-interview-prep` OOP and SQL sections; review your own project for resume Q&A |
| ⚪ Skip | Don't start new topics you've never touched in the last 48 hours |
