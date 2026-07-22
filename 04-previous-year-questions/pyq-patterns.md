# Previous-Year Question Patterns

Important: these are **paraphrased patterns and approach notes**, not copy-pasted problem statements — treat them as "what shape of problem to expect," then go practice the underlying pattern on LeetCode/GfG rather than memorizing an exact statement. Infosys reuses *patterns* year to year, not verbatim questions.

## Pattern 1 — Modular arithmetic / number theory framing

**Shape**: You're given a number `N` and asked to find some property of a subset of integers in a range, expressed under modular arithmetic (e.g., "find the largest subset whose product is 1 mod N").

**Underlying skill tested**: modular exponentiation, multiplicative order, basic number theory — not raw brute force.

**How to practice**: GfG's "Modular Arithmetic" section; LeetCode problems tagged `math` + `number-theory`.

## Pattern 2 — "Rearrange array into two groups with minimum adjacent swaps"

**Shape**: Given an array, rearrange it so all elements satisfying some condition (even/odd, positive/negative, above/below a threshold) end up grouped together — using the *minimum number of adjacent swaps*.

**Underlying skill tested**: two-pointer technique, greedy counting (you usually don't need to simulate the swaps — you can count inversions/mismatches directly).

**How to practice**: LeetCode "minimum swaps to group all 1s together" and its variants.

## Pattern 3 — Probability / simulation with expected value

**Shape**: A probability question involving drawing items (balls, cards) from a container, asking for the probability of some final-state event across multiple categories.

**Underlying skill tested**: basic combinatorics, expected value reasoning, careful precision handling (answers often allow small absolute/relative error tolerance — read the output-format constraints carefully).

**How to practice**: GfG "probability and expected value" problems; pay special attention to how the problem defines acceptable error tolerance in the output.

## Pattern 4 — XOR-maximization / selection under a size constraint

**Shape**: Given an array, choose at most `N/2` elements to maximize (or achieve a target) XOR of the chosen subset.

**Underlying skill tested**: bitmasking, sometimes a greedy bit-by-bit construction (decide each bit from the most significant down), or DP over subsets for smaller constraints.

**How to practice**: LeetCode/GfG problems tagged `bit-manipulation` + `subset`; specifically look at "maximum XOR subset" style problems.

## Pattern 5 — Base conversion

**Shape**: Convert a number from decimal into a different base `K`, sometimes framed indirectly (e.g., describing a positional numeral system and asking you to reconstruct the representation).

**Underlying skill tested**: careful implementation of repeated division/remainder logic, off-by-one handling for the leading digit.

**How to practice**: straightforward — implement base conversion for a few different bases from scratch without a library function, so you're fast under time pressure.

## General notes on the question bank

- Across previous years, at least one question per set tends to be a straightforward Easy/Medium DSA problem (arrays, strings, stacks/queues) — don't over-index prep time on the exotic patterns above at the expense of fundamentals.
- Questions are pulled from a large rotating bank — expect the *style* above, not these exact five problems.
- Where to go deeper: the GitHub repo `karthikreddy-7/Infosys-SP-Coding-Questions` and PrepInsta's coding-questions page both maintain larger, regularly updated banks of these patterns with worked solutions — see `06-resources/sources.md` for links.
