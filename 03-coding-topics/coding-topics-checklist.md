# Coding Round — Full Topic Checklist

Organized by the same Easy / Medium / Hard split the actual coding round uses, so you can practice in the order you'll be tested.

## Easy (Q1-tier)

Focus: correctness, clean logic-building, boundary condition safety, and linear time efficiency.

- [ ] **Arrays** — traversal, array rotation in-place, prefix sums, two-pointer basics, sliding window basics
  - *Practice Prompt*: Given an array, find the maximum sum of any contiguous subarray of size $K$. (Sliding Window)
  - *Practice Prompt*: Rotate an array of $N$ elements to the right by $K$ steps in $O(1)$ extra space.
  - *Evaluator Cue*: Check for $O(N)$ time and $O(1)$ auxiliary space solutions; handle empty arrays or $K > N$.
- [ ] **Strings** — palindrome checks, anagram checks, string reversal/manipulation, pattern matching basics
  - *Practice Prompt*: Determine if two strings are anagrams of each other after removing non-alphanumeric characters.
  - *Practice Prompt*: Find the first non-repeating character in a string in a single pass.
  - *Evaluator Cue*: Watch for case-sensitivity, ASCII vs. Unicode, and boundary strings of length 0 or 1.
- [ ] **Stacks & Queues** — balanced parentheses, next-greater-element, circular queue, basic simulation problems
  - *Practice Prompt*: Given a string of parentheses `()[]{}` check if the input string is valid.
  - *Practice Prompt*: Implement a Min-Stack that supports `getMin()` in $O(1)$ time.
  - *Evaluator Cue*: Ensure stack underflow/overflow handling; avoid $O(N^2)$ brute-force lookup for Next Greater Element.
- [ ] **Hash Maps & Sets** — frequency counting, two-sum style lookups, intersection/union of arrays
  - *Practice Prompt*: Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.
  - *Practice Prompt*: Count the frequency of each element and return elements appearing more than $\lfloor N/3 \rfloor$ times.
  - *Evaluator Cue*: Leverage $O(1)$ average lookup time; handle duplicate key collisions properly.
- [ ] **Linked Lists** — reversal, cycle detection (Floyd's Tortoise and Hare), merging two sorted lists, basic insert/delete
  - *Practice Prompt*: Reverse a singly linked list iteratively and recursively.
  - *Practice Prompt*: Detect if a linked list has a cycle and find the node where the cycle begins.
  - *Evaluator Cue*: Watch out for `NullPointerException` / segmentation faults when accessing `node.next.next`.
- [ ] **Heaps & Priority Queue Basics** — k-th largest element, min-heap insertion/extraction
  - *Practice Prompt*: Find the $K$-th largest element in an unsorted array using a Min-Heap of size $K$.
  - *Evaluator Cue*: Ensure $O(N \log K)$ runtime complexity rather than full sorting $O(N \log N)$.

## Medium (Q2-tier)

Focus: choosing the optimal technique, avoiding brute force, reducing time complexity from $O(N^2)$ to $O(N \log N)$ or $O(N)$.

- [ ] **Greedy Algorithms** — interval scheduling, activity selection, coin-change (greedy variant), minimum-swaps-style problems
  - *Practice Prompt*: Given $N$ activities with start and finish times, select the maximum number of activities that can be performed by a single person.
  - *Practice Prompt*: Given an array of $0$s and $1$s, find the minimum number of adjacent swaps required to group all $1$s together.
  - *Evaluator Cue*: Prove greedy choice property; sort intervals by end time rather than start time.
- [ ] **Advanced Sliding Window & Two Pointers** — variable-length sliding window, 3-Sum / 4-Sum
  - *Practice Prompt*: Find the length of the longest substring without repeating characters.
  - *Practice Prompt*: Find all unique triplets in an array that sum to zero.
  - *Evaluator Cue*: Handle shrinking window condition cleanly without infinite loop.
- [ ] **Monotonic Stack & Queue** — daily temperatures, sliding window maximum, largest rectangle in histogram
  - *Practice Prompt*: For each day, find how many days you would have to wait until a warmer temperature.
  - *Evaluator Cue*: Maintain monotonic ordering ($O(N)$ total push/pop operations).
- [ ] **Recursion & Backtracking** — subset generation, permutations, N-Queens, Sudoku solver, combination sum with constraints
  - *Practice Prompt*: Generate all unique combinations of numbers that sum up to a target value where elements can be reused.
  - *Practice Prompt*: Solve N-Queens problem and return total count of distinct valid board configurations.
  - *Evaluator Cue*: Prune invalid recursive branches early to prevent TLE (Time Limit Exceeded).
- [ ] **Trees & Binary Search Trees (BST)** — tree traversals (in/pre/post-order), BFS level-order, height/diameter, Lowest Common Ancestor (LCA)
  - *Practice Prompt*: Calculate the diameter of a binary tree (longest path between any two nodes).
  - *Practice Prompt*: Find the Lowest Common Ancestor (LCA) of two given nodes in a Binary Tree.
  - *Evaluator Cue*: Handle unbalanced / skewed trees ($O(H)$ space for recursion stack).
- [ ] **Optimization & Greedy/DP Hybrid** — minimize/maximize operations framing (recurring Infosys phrasing)
  - *Practice Prompt*: Minimum operations to reduce a number to 1 using allowed operations (subtract 1, divide by 2, divide by 3).
  - *Evaluator Cue*: Identify whether greedy choice works or if subproblem overlap requires memoization.

## Hard (Q3-tier)

Focus: recognizing subproblem overlap, complex state space representation, graph modeling, and advanced algorithmic patterns under time pressure.

- [ ] **Dynamic Programming (1D & 2D)** — climbing stairs, house robber, 0/1 Knapsack, Unbounded Knapsack, Longest Common Subsequence (LCS), Longest Increasing Subsequence (LIS), Edit Distance, Grid Path Min Cost
  - *Practice Prompt*: Given two strings `str1` and `str2`, return the minimum number of operations (insert, delete, replace) to convert `str1` to `str2`.
  - *Practice Prompt*: Find the length of the longest subsequence in an array such that all elements of the subsequence are sorted in strictly increasing order.
  - *Practice Prompt*: Find the maximum profit from selecting items with given weights and values subject to a total capacity $W$.
  - *Evaluator Cue*: State definition $DP[i][j]$ must be precise; space-optimize from 2D $O(N \times M)$ to 1D $O(M)$ where possible.
- [ ] **Graph Algorithms** — BFS/DFS traversal, connected components, cycle detection (directed/undirected), Shortest Path (Dijkstra, BFS on unweighted graph), Topological Sort (Kahn's algorithm)
  - *Practice Prompt*: Find the shortest path from a source node to all other nodes in a weighted graph with non-negative edge weights (Dijkstra).
  - *Practice Prompt*: Given $N$ courses and prerequisite pairs, determine if it is possible to finish all courses (Topological Sort / Cycle Detection).
  - *Evaluator Cue*: Use adjacency lists over adjacency matrices for sparse graphs; maintain visited arrays/sets to prevent cycles.
- [ ] **Disjoint Set Union (DSU / Union-Find)** — Kruskal's MST, connected components, redundant connection detection
  - *Practice Prompt*: Given a graph that started as a tree with $N$ nodes and had one extra edge added, find the redundant edge that can be removed.
  - *Evaluator Cue*: Implement path compression and union by rank/size ($O(\alpha(N))$ per operation).
- [ ] **Bit Manipulation & Bitmasking** — XOR subset problems, counting set bits (Brian Kernighan's), DP with bitmasking
  - *Practice Prompt*: Given an array where every element appears twice except for two elements that appear only once, find those two unique elements in $O(N)$ time and $O(1)$ space.
  - *Practice Prompt*: Find the maximum XOR value of any two numbers in an array.
  - *Evaluator Cue*: Beware of integer bit-width overflow (use 64-bit integer types `long long` / `long` when shifting $> 31$ bits).
- [ ] **Number Theory Basics** — modular exponentiation, GCD/LCM (Euclidean Algorithm), Sieve of Eratosthenes, base conversion
  - *Practice Prompt*: Compute $(A^B) \pmod C$ efficiently for large integers $A, B, C$.
  - *Practice Prompt*: Convert an integer into its representation in an arbitrary base $K$ ($2 \le K \le 36$).
  - *Evaluator Cue*: Handle negative numbers and modular subtraction safely: `(a % m + m) % m`.
- [ ] **Advanced Data Structures (SP-Tier)** — Trie (Prefix Tree), Segment Tree / Fenwick Tree (Binary Indexed Tree)
  - *Practice Prompt*: Implement a Trie with `insert`, `search`, and `startsWith` methods.
  - *Practice Prompt*: Range Sum Query with point updates using a Segment Tree or Fenwick Tree.
  - *Evaluator Cue*: Memory cleanup in Trie nodes; 1-based indexing clarity in Fenwick trees.

## Cross-cutting skills (test throughout, not a separate section)

- [ ] Time and space complexity analysis — be ready to state Big-O for every solution you write, unprompted
- [ ] Writing edge-case-safe code (empty input, single element, all-same-elements, overflow-prone inputs)
- [ ] Clean variable naming and function decomposition — interviewers do look at code quality, not just test-case pass rate

## DSE-specific additions

If you're targeting DSE specifically, layer these on top of the DSA checklist above:

- [ ] REST API basics — writing a GET/POST endpoint in your primary framework (a real recent DSE interview question involved writing basic FastAPI/Express endpoints)
- [ ] SQL — joins, aggregations, subqueries, window functions (cross-reference with Section 05 interview bank)
- [ ] OOP fundamentals — the four pillars, applied to a real design question, not just definitions
- [ ] Git workflow — be ready to describe your actual workflow (branching, merging, resolving conflicts), not just name the commands
- [ ] System Architecture Awareness — client-server communication, JSON payload design, stateless vs. stateful authentication (JWT basics), database choice tradeoffs (SQL vs. NoSQL)
