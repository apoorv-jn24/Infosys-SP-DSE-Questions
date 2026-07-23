# Syllabus and Exam Pattern

## Marks Breakdown

| Question | Difficulty | Marks | Topic Area | Target Time |
|---|---|---|---|---|
| **Q1** | Easy | 20 | Arrays, Strings, Basic Data Structures | 35–40 min |
| **Q2** | Medium | 30 | Greedy, Sliding Window, Trees, Heaps | 50–55 min |
| **Q3** | Hard | 50 | Dynamic Programming, Bit Manipulation, Graphs | 65–75 min |

Total: **3 questions · 100 marks · 3 hours.**

---

## Topic Blueprint

Frequency of topic appearance across recent Infosys SP/DSE exam slots:

| Topic | Frequency | Notes |
|---|---|---|
| Dynamic Programming | ⬛⬛⬛⬛⬛ Very High | Grid DP, Subset DP, Counting DP, LCS/LIS variants |
| Bit Manipulation | ⬛⬛⬛⬛⬜ High | XOR properties, MSB tricks, bitmask DP |
| Greedy + Sorting | ⬛⬛⬛⬛⬜ High | Interval scheduling, exchange arguments, sorting-based optimal choices |
| Arrays & Two Pointers | ⬛⬛⬛⬜⬜ Medium-High | Prefix sums, sliding window, two-pointer partitioning |
| Number Theory | ⬛⬛⬛⬜⬜ Medium | Modular arithmetic, base conversion, Euler's totient |
| Graphs / BFS / DFS | ⬛⬛⬛⬜⬜ Medium | Connected components, shortest paths, grid traversal |
| Stacks & Queues | ⬛⬛⬜⬜⬜ Low-Medium | Monotonic stack, next greater element, balanced brackets |
| Probability | ⬛⬜⬜⬜⬜ Low | Combinatorics, expected value |

---

## Strategy in the Room (3-Hour Window)

| Time | Action |
|---|---|
| **0:00 – 0:10** | Read all 3 questions in full. Identify which is Easy / Medium / Hard. |
| **0:10 – 0:50** | Solve Q1 completely. Run all sample cases. Handle edge cases. |
| **0:50 – 1:45** | Solve Q2. Identify optimal technique (Greedy / DP / Sliding Window). |
| **1:45 – 2:45** | Attack Q3. If optimal solution is unclear, write a memoized brute-force for partial credit. |
| **2:45 – 3:00** | Re-run edge cases. Remove debug print statements. Check for overflow. |

**Avoid $O(N^2)$ when $N > 10^4$.** Infosys test cases are designed to time-out naive solutions at $N = 10^5$.

---

## 5 High-Cost Exam Mistakes

These mistakes are the most common reasons candidates lose marks on problems they *understand*:

### Mistake 1 — 32-bit Integer Overflow
**What happens**: An accumulator (running sum, product, count) exceeds $2^{31} - 1 \approx 2.1 \times 10^9$.  
**Fix**: In C++, always default accumulators to `long long`. In Python, integers are arbitrary precision — no action needed. In Java, use `long` for large sums.

```cpp
// Wrong — int overflow when N=10^5 and values are ~10^9
int total = 0;
for (int x : arr) total += x;

// Correct
long long total = 0;
for (int x : arr) total += x;
```

### Mistake 2 — $O(N^2)$ TLE on Large Inputs
**What happens**: A nested loop solution passes sample cases (small $N$) but times out on hidden cases ($N = 10^5$).  
**Fix**: Identify the optimal technique (sorting, hash map, prefix sum, sliding window) before coding.

### Mistake 3 — Recursion Stack Overflow on DFS
**What happens**: DFS on a large grid ($1000 \times 1000$) blows the call stack with recursive calls.  
**Fix**: Use iterative BFS with an explicit queue, or in Python set `sys.setrecursionlimit(10**6)` before the solution.

### Mistake 4 — Misreading Constraints
**What happens**: "at most $K$" vs "exactly $K$" vs "at most $N/2$" — wrong condition leads to wrong answers on edge-case test cases.  
**Fix**: Spend 2 minutes rereading the constraint section specifically. Write the constraint as a variable in your code comments.

### Mistake 5 — Untested Edge Cases
**What happens**: Solution passes sample but fails on $N=1$, all-negative values, $K > N$, or empty input.  
**Fix**: Before submitting each question, manually trace through: single element, all same elements, maximum constraint, empty/null input.

---

## Language Choice: Python vs C++

| Factor | Python 3 | C++ 17 |
|---|---|---|
| Speed | ~5–10× slower | Fastest |
| Integer overflow | No issue (arbitrary precision) | Must use `long long` |
| STL / standard library | `collections`, `heapq`, `functools` | Full C++ STL (`priority_queue`, `unordered_map`, etc.) |
| Recursion limit | Must set `sys.setrecursionlimit(10**6)` | Stack-limited (~1M frames by default) |
| I/O speed | Use `sys.stdin.readline` for large input | Use `cin.tie(NULL)`, `ios::sync_with_stdio(false)` |
| Recommendation | **Preferred for DP and algorithm clarity** | **Preferred when TLE is a risk** |

---

## Supported Languages

C, C++, Java, Python 3, JavaScript (Node.js).

---

## Off-Campus MCQ Sections

Generic off-campus drives (not HackWithInfy) may include non-coding MCQ sections:

| Section | Questions | Time | Topics |
|---|---|---|---|
| Mathematical Ability | ~10 | 35 min | Percentages, Probability, P&C, Speed-Distance |
| Logical Reasoning | ~15 | 25 min | Syllogisms, Seating Arrangement, Coding-Decoding |
| Verbal Ability | ~20 | 20 min | Reading Comprehension, Error Spotting, Sentence Correction |
| Pseudocode / Technical MCQ | ~5–10 | — | Code output tracing, pointer arithmetic, Big-O |

---

## Prep Time Allocation

- **~65–70%** → Coding topics + problem practice (Sections 03–04)
- **~25–30%** → Technical interview prep: DSA/OOP/SQL (Section 05)
- **~5%** → HR and behavioral prep
