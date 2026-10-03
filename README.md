# Infosys SP & DSE Preparation Guide

A structured, self-contained study guide for the Infosys **Specialist Programmer (SP)** and **Digital Specialist Engineer (DSE)** hiring process: exam pattern, a coding-topic checklist, 20 pattern-based coding problems solved in **Python 3 and C++17**, and technical + HR interview prep.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/)
[![C++ 17](https://img.shields.io/badge/C%2B%2B-17-purple.svg)](https://isocpp.org/)

> [!IMPORTANT]
> Problem statements are **paraphrased from public candidate reports**, not official Infosys papers. Exam patterns change from batch to batch. Your official Infosys invitation email takes priority over anything here.

---

## What's Inside

| Folder | Contents |
|---|---|
| [`01-overview/`](01-overview/overview.md) | SP vs DSE distinctions, reported salary bands, hiring stages, HackWithInfy vs campus routes, role self-assessment |
| [`02-syllabus-and-pattern/`](02-syllabus-and-pattern/syllabus-and-pattern.md) | 3-question / 100-mark pattern (20/30/50), topic blueprint, time plan, 5 high-cost exam mistakes, Python vs C++ |
| [`03-coding-topics/`](03-coding-topics/coding-topics-checklist.md) | Topic checklist by tier, 4-week plan, prerequisites, DSE additions, last-48-hours plan |
| [`04-previous-year-questions/`](04-previous-year-questions/pyq-patterns.md) | 19 core assessment patterns + 20 solved problems (statement, insight, complexity, Python, C++, edge cases) |
| [`05-interview-prep/`](05-interview-prep/interview-prep.md) | OOP (30), SQL/DBMS (20), OS/CN notes, HR prompts (20), mock interview scenarios |
| [`06-resources/`](06-resources/sources.md) | External guides, repos, playlists, official Infosys links |

---

## 20 Solved Problems — Master Index

| # | Problem | Tier | Marks | Topic | File |
|---|---|---|---|---|---|
| 1 | Maximum Subarray Sum | Easy | 20 | Kadane's algorithm | [→](04-previous-year-questions/01-maximum-subarray-sum.md) |
| 2 | Next Greater Element | Easy | 20 | Monotonic stack | [→](04-previous-year-questions/02-next-greater-element.md) |
| 3 | Rotate Array by K | Easy | 20 | Reversal ($O(1)$ space) | [→](04-previous-year-questions/03-rotate-array-by-k.md) |
| 4 | Summer Array: Min Swaps ⚠️ | Easy | 20 | Inversion count ($O(N \log N)$) | [→](04-previous-year-questions/04-summer-array-min-swaps.md) |
| 5 | Min Base with Identical Digits ⚠️ | Easy | 20 | Number theory & divisor scan | [→](04-previous-year-questions/05-min-base-identical-digits.md) |
| 6 | Monster Quest | Medium | 30 | Greedy + two pointers | [→](04-previous-year-questions/06-monster-quest.md) |
| 7 | Andy's Vacation | Medium | 30 | Streak counting | [→](04-previous-year-questions/07-andys-vacation.md) |
| 8 | Min Ugliness of Binary String ⚠️ | Medium | 30 | Runs + regret-greedy queue | [→](04-previous-year-questions/08-min-ugliness-binary-string.md) |
| 9 | Trapping Rain Water | Medium | 30 | Two pointers prefix-max | [→](04-previous-year-questions/09-trapping-rain-water.md) |
| 10 | Number of Islands | Medium | 30 | BFS on grid | [→](04-previous-year-questions/10-number-of-islands.md) |
| 11 | Coin Change | Medium | 30 | Unbounded knapsack DP | [→](04-previous-year-questions/11-coin-change.md) |
| 12 | Max Subset XOR ≤ K ⚠️ | Medium | 30 | Linear XOR basis + Gauss-Jordan | [→](04-previous-year-questions/12-max-xor-sum-in-range.md) |
| 13 | Longest Common Subsequence | Hard | 50 | 2D DP (rolling row) | [→](04-previous-year-questions/13-longest-common-subsequence.md) |
| 14 | Counting Divisible Arrays ⚠️ | Hard | 50 | CRT + polynomial exponentiation | [→](04-previous-year-questions/14-counting-divisible-arrays.md) |
| 15 | Packing Gifts into K Boxes ⚠️ | Hard | 50 | Binary search on answer | [→](04-previous-year-questions/15-packing-gifts-into-k-boxes.md) |
| 16 | Longest Increasing Path in Matrix | Hard | 50 | DP on DAG (memoized DFS) | [→](04-previous-year-questions/16-longest-increasing-path-matrix.md) |
| 17 | Max XOR of Half-Sized Subset | Hard | 50 | Subset enumeration / basis | [→](04-previous-year-questions/17-max-xor-half-sized-subset.md) |
| 18 | Longest Bitwise-Compatible LIS ⚠️ | Hard | 50 | MSB transform + patience LIS | [→](04-previous-year-questions/18-longest-bitwise-compatible-lis.md) |
| 19 | Largest Set with Product 1 mod N ⚠️ | Hard | 50 | Totient + primitive root parity | [→](04-previous-year-questions/19-largest-set-product-1-mod-n.md) |
| 20 | Balls and Buckets Probability | Hard | 50 | Convolution DP | [→](04-previous-year-questions/20-balls-and-buckets-probability.md) |

> ⚠️ = Problems where widely circulated online solutions contain documented errors (bubble sort timeouts, wrong sample outputs, or flawed group theory). Correct formulations and mathematical proofs are provided.

---

## Input Format Convention

The **Python and C++ solutions read the same input format**: the first line holds sizes/parameters (`n`, `K`, …) and the following lines hold the data. Each file lists its exact format under *Sample Input*.

---

## Recommended 4-Week Plan

| Week | Focus | Material |
|---|---|---|
| **Week 1** | Exam pattern, role choice, Easy-tier topics | `01`, `02`, `03` (Easy), Problems 1–5 |
| **Week 2** | Medium tier: greedy, sliding window, BFS, DP basics | `03` (Medium), Problems 6–12 |
| **Week 3** | Hard tier: DP, bit manipulation, number theory | `03` (Hard), Problems 13–20 |
| **Week 4** | Interview prep, mock rounds, revision | `05`, re-solve Problems 4, 5, 8, 12, 14, 15, 18, 19 |

**Key Principles:**
1. **The coding round is the hardest filter.** Dedicate ~65–70% of prep time to Sections 03–04.
2. **Infosys reuses patterns, not exact problems.** Master the underlying technique.
3. **Attempt all 3 questions.** Partial scoring exists on hidden test cases — never leave a question blank.

---

## Progress Tracker

- [ ] Reviewed exam pattern and marks breakdown
- [ ] Completed Easy tier + Problems 1–5
- [ ] Completed Medium tier + Problems 6–12
- [ ] Completed Hard tier + Problems 13–20
- [ ] Technical interview prep (DSA / OOP / SQL / OS / CN)
- [ ] HR round prep
- [ ] Conducted timed 3-hour mock assessment

---

## Contributing

Found an issue or want to contribute a new problem pattern? Please review [CONTRIBUTING.md](CONTRIBUTING.md).

---

## License

This project is licensed under the [MIT License](LICENSE).
