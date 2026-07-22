# Syllabus and Exam Pattern

## Coding round structure

- **3 coding questions, 3 hours total.**
- Each question is drawn from a **different topic** and pitched at a **different difficulty level** — the round is deliberately spread, not three problems of the same type.
- Typical split reported across sources:
  - **Q1 — Easy**: arrays/strings, basic data structures (stacks, queues, hash maps, linked lists). Tests basic logic-building and correctness.
  - **Q2 — Medium**: greedy algorithms, recursion, backtracking, or optimization-style problems requiring some analytical thinking.
  - **Q3 — Hard**: dynamic programming or graph-based problems, testing advanced algorithmic skill.
- **Passing all test cases is not mandatory** for every question — partial credit exists — but there can be **sectional/topical cutoffs**, meaning you can't skip a section entirely and rely on the other two carrying you. Attempt all three.
- Time management matters more than raw difficulty: with 3 hours for 3 questions, a common strategy is ~45–50 minutes on Q1, ~60 on Q2, and the remainder on Q3, leaving buffer for edge-case testing.

## Strategic Time-Budget Allocation (3-Hour Coding Test)

| Phase | Target Duration | Goal | Focus / Strategy |
|---|---|---|---|
| **Question 1 (Easy)** | 30–45 mins | 100% test cases passed | Read carefully, handle edge cases (empty input, single element, negative numbers, integer overflow). |
| **Question 2 (Medium)** | 50–60 mins | Full or major partial score | Identify optimal technique (Greedy, Two Pointers, Sliding Window, Prefix Sum). Avoid naive $O(N^2)$ if $N > 10^4$. |
| **Question 3 (Hard)** | 60–75 mins | Maximize test cases | Formulate DP state transitions or Graph algorithms (BFS/DFS/Dijkstra). If optimal solution is tough, implement a memoized recursion or partial greedy solution for partial credit. |
| **Review & Edge Testing** | 15–20 mins | Prevent silent failures | Verify boundary conditions, large $N$ limits, print statements removed, clean memory/variables. |

## Supported Programming Languages & Environment

- **Languages Allowed**: C, C++, Java, Python (Python 3), and JavaScript (Node.js).
- **Standard Library Capabilities**:
  - **C++**: Full C++ STL support (`std::vector`, `std::unordered_map`, `std::priority_queue`, `std::set`, `std::algorithm`). Fast I/O (`cin.tie(NULL)`) recommended.
  - **Java**: Standard Java Collection Framework (`ArrayList`, `HashMap`, `PriorityQueue`, `TreeSet`). Use `FastScanner` or `BufferedReader` for large input sizes.
  - **Python**: Standard modules available (`collections.deque`, `collections.Counter`, `heapq`, `functools.lru_cache`, `sys.setrecursionlimit`). Watch out for recursion depth limits in Graph/DP problems.

## Platform & Assessment Logistics

- **Platform Rules**: Tests are conducted on platforms such as HackerEarth, CoCubes, or Infosys' internal assessment portal.
- **No-Back-Navigation / Sectional Restrictions**: In certain assessment formats, once you submit a question or move between sections, returning to previous questions may be restricted. Always confirm navigation rules in the test instructions before starting.
- **Webcam & Screen Proctoring**: Automated AI proctoring logs tab switching, secondary screens, and audio. Keep your workspace clear.

## Off-Campus / Generic Hiring Aptitude & MCQ Sections

While HackWithInfy and pure SP/DSE drives focus 100% on coding, generic off-campus hiring drives or initial qualifying rounds may include non-coding MCQ sections prior to or alongside coding:

1. **Mathematical Ability**: ~10 questions / 35 mins (Percentages, Profit & Loss, Permutations & Combinations, Probability, Speed-Distance-Time).
2. **Logical Reasoning**: ~15 questions / 25 mins (Syllogisms, Data Sufficiency, Coding-Decoding, Seating Arrangement Puzzles).
3. **Verbal Ability**: ~20 questions / 20 mins (Reading Comprehension, Error Spotting, Sentence Correction, Critical Reasoning).
4. **Pseudocode / Technical MCQs**: ~5–10 questions on code output tracing, pointer arithmetic, and algorithmic complexity.

## Round-by-round flow

1. **Online coding assessment** (see above) — the primary filter.
2. **Technical interview** — if you clear the coding round, this is comparable in difficulty to any solid campus technical interview: DSA fundamentals, OOP, SQL, and resume/project deep-dives.
3. **HR round** — standard behavioral/fit round.

## What differs between SP and DSE at the syllabus level

- **SP**: heavier weight on algorithmic questions (DP, graphs) even at the "coding round" stage; interview probes deeper into complexity analysis and algorithm choice tradeoffs.
- **DSE**: coding round difficulty is moderate; interview leans into full-stack/digital skills — frameworks, REST APIs, cloud/automation concepts, and how you built your projects, not just algorithm design.

## Exam logistics notes

- Infosys hiring (on-campus or off-campus/HackWithInfy-style drives) does **not run on a fixed public schedule** — dates depend on organizational hiring needs, so always confirm timing through your registered email/campus placement cell rather than assuming a fixed annual calendar.
- Eligibility criteria (branch, CGPA, backlog rules) are set per drive — check the official notification for your batch rather than relying on last year's numbers.

## Prep-time allocation (recommended)

Given that the coding round is consistently flagged as the harder filter:

- **~65–70%** of prep time → coding topics + previous-year pattern practice (Sections 03–04)
- **~25–30%** of prep time → technical interview prep: DSA/OOP/SQL revision, resume Q&A (Section 05)
- **~5%** → HR/behavioral prep
