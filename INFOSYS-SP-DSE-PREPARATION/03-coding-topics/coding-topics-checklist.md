# Coding Round — Full Topic Checklist

Organized by the same Easy / Medium / Hard split the actual coding round uses, so you can practice in the order you'll be tested.

## Easy (Q1-tier)

Focus: correctness and clean logic-building, not cleverness.

- [ ] Arrays — traversal, rotation, prefix sums, two-pointer basics, sliding window basics
- [ ] Strings — palindrome checks, anagram checks, string reversal/manipulation, pattern matching basics
- [ ] Stacks — balanced parentheses, next-greater-element, basic expression evaluation
- [ ] Queues — circular queue, basic simulation problems
- [ ] Hash maps — frequency counting, two-sum style lookups
- [ ] Linked lists — reversal, cycle detection, merging two sorted lists, basic insert/delete

## Medium (Q2-tier)

Focus: choosing the right technique, not just brute force.

- [ ] Greedy algorithms — interval scheduling, activity selection, coin-change (greedy variant), minimum-swaps-style problems
- [ ] Recursion — generating subsets/permutations, divide-and-conquer basics
- [ ] Backtracking — N-Queens style, combination/subset generation with constraints, Sudoku-style constraint problems
- [ ] Optimization problems — problems with a "minimize/maximize X operations" framing (a recurring Infosys phrasing pattern — see Section 04)
- [ ] Trees — binary tree traversals (in/pre/post-order), BST operations, height/diameter problems

## Hard (Q3-tier)

Focus: recognizing the underlying pattern under time pressure.

- [ ] Dynamic programming — 1D DP (climbing stairs, house robber style), 2D DP (grid paths, edit distance), knapsack variants, subsequence problems (LCS, LIS)
- [ ] Graphs — BFS/DFS traversal, connected components, shortest path (Dijkstra/BFS on unweighted graphs), cycle detection, topological sort
- [ ] Bit manipulation — XOR-based problems (a recurring Infosys pattern — see Section 04), bitmasking for subset problems
- [ ] Number theory basics — modular arithmetic, GCD/LCM, base conversion problems (also a recurring pattern)

## Cross-cutting skills (test throughout, not a separate section)

- [ ] Time and space complexity analysis — be ready to state Big-O for every solution you write, unprompted
- [ ] Writing edge-case-safe code (empty input, single element, all-same-elements, overflow-prone inputs)
- [ ] Clean variable naming and function decomposition — interviewers do look at code quality, not just test-case pass rate

## DSE-specific additions

If you're targeting DSE specifically, layer these on top of the DSA checklist above:

- [ ] REST API basics — writing a GET/POST endpoint in your primary framework (a real recent DSE interview question involved writing basic FastAPI endpoints)
- [ ] SQL — joins, aggregations, subqueries, window functions (see your `sql-notes-repo` for the deep dive)
- [ ] OOP fundamentals — the four pillars, applied to a real design question, not just definitions
- [ ] Git workflow — be ready to describe your actual workflow (branching, merging, resolving conflicts), not just name the commands
