# Problem 8 — Minimum Ugliness of Binary String

**Tier**: Medium (Q2) | **Marks**: 30 | **Topic**: Greedy / Sliding Window

---

## Problem

Given a binary string $S$ of length $N$ and an integer $K$, you can flip **at most $K$ characters** (0→1 or 1→0). The **ugliness** of a string is the number of adjacent pairs where the two characters differ (i.e., the number of `01` or `10` transitions). Find the minimum possible ugliness after at most $K$ flips.

**Sample Input**:
```
S = "010101"
K = 1
```
**Sample Output**:
```
4
```

**Constraints**: $1 \leq N \leq 10^5$, $0 \leq K \leq N$.

---

## Key Insight

> Ugliness = number of "boundary" positions between blocks of identical characters. Flipping a contiguous block of $K$ characters into the same value merges adjacent blocks, reducing boundaries by 2 per merged boundary (left and right of the flipped region). Use a **sliding window of width $K$** and count boundary reductions.

---

## Approach

1. Precompute total ugliness (transitions in original string).
2. Use a sliding window of length $K$ across the string.
3. For each window, count how many boundaries it contains inside + how boundaries at window edges change.
4. Track the maximum reduction in ugliness achievable.
5. Answer = `initial_ugliness - max_reduction`.

**Complexity**: $O(N)$ time, $O(1)$ space.

---

## Python 3

```python
def min_ugliness(S, K):
    n = len(S)
    # Count initial ugliness
    total = sum(S[i] != S[i+1] for i in range(n-1))
    if K == 0 or total == 0:
        return total

    # Sliding window: count internal boundaries in window [i, i+K-1]
    # A flip of whole window can remove left+right boundary of window
    best_reduction = 0
    # Count boundaries inside window of size K
    internal = sum(S[i] != S[i+1] for i in range(K-1))

    for start in range(n - K + 1):
        # boundaries saved = left edge + right edge saved
        left_save  = 1 if start > 0 and S[start-1] != S[start] else 0
        right_save = 1 if start+K < n and S[start+K-1] != S[start+K] else 0
        best_reduction = max(best_reduction, left_save + right_save)

        # Slide window
        if start + K < n:
            internal -= (S[start] != S[start+1])
            internal += (S[start+K-1] != S[start+K])

    return total - best_reduction

S = input().strip()
K = int(input())
print(min_ugliness(S, K))
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    string S; int K;
    cin >> S >> K;
    int n = S.size();

    int total = 0;
    for (int i = 0; i < n-1; i++) total += (S[i] != S[i+1]);

    if (K == 0 || total == 0) { cout << total << "\n"; return 0; }

    int best = 0;
    for (int start = 0; start + K <= n; start++) {
        int left  = (start > 0   && S[start-1] != S[start])   ? 1 : 0;
        int right = (start+K < n && S[start+K-1] != S[start+K]) ? 1 : 0;
        best = max(best, left + right);
    }
    cout << total - best << "\n";
    return 0;
}
```

---

## Edge Cases

| Input | K | Output |
|---|---|---|
| `"0000"` | 2 | `0` |
| `"0101"` | 4 | `0` (flip all → `0000` or `1111`) |
| `"01"` | 1 | `0` |
