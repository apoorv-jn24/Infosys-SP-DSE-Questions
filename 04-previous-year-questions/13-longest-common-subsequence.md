# Problem 13 — Longest Common Subsequence

**Tier**: Hard (Q3) | **Marks**: 50 | **Topic**: Dynamic Programming (2D)

---

## Problem

Given two strings $A$ and $B$, find the length of their **Longest Common Subsequence (LCS)** — the longest sequence of characters that appear in the same order in both strings (not necessarily contiguous).

**Sample Input**:
```
A = "ABCBDAB"
B = "BDCAB"
```
**Sample Output**:
```
4
```
**Explanation**: LCS = `"BCAB"` or `"BDAB"` (length 4).

**Constraints**: $1 \leq |A|, |B| \leq 1000$.

---

## Key Insight

> Classic 2D DP. `dp[i][j]` = LCS length of `A[:i]` and `B[:j]`. Recurrence: if `A[i-1] == B[j-1]`, then `dp[i][j] = dp[i-1][j-1] + 1`; else `dp[i][j] = max(dp[i-1][j], dp[i][j-1])`.

Space-optimize to $O(\min(|A|, |B|))$ using two rolling rows.

---

## Approach

1. `dp = [[0] * (|B|+1)] * (|A|+1)`.
2. For `i = 1...|A|`, `j = 1...|B|`:
   - If `A[i-1] == B[j-1]`: `dp[i][j] = dp[i-1][j-1] + 1`.
   - Else: `dp[i][j] = max(dp[i-1][j], dp[i][j-1])`.
3. Return `dp[|A|][|B|]`.

**Complexity**: $O(|A| \times |B|)$ time, $O(|B|)$ space (rolling row).

---

## Python 3

```python
def lcs(A, B):
    m, n = len(A), len(B)
    # Space-optimized: 1D rolling array
    prev = [0] * (n + 1)
    for i in range(1, m + 1):
        curr = [0] * (n + 1)
        for j in range(1, n + 1):
            if A[i-1] == B[j-1]:
                curr[j] = prev[j-1] + 1
            else:
                curr[j] = max(prev[j], curr[j-1])
        prev = curr
    return prev[n]

A = input().strip()
B = input().strip()
print(lcs(A, B))
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false); cin.tie(NULL);
    string A, B; cin >> A >> B;
    int m = A.size(), n = B.size();

    vector<int> prev(n+1, 0), curr(n+1, 0);
    for (int i = 1; i <= m; i++) {
        fill(curr.begin(), curr.end(), 0);
        for (int j = 1; j <= n; j++) {
            if (A[i-1] == B[j-1]) curr[j] = prev[j-1] + 1;
            else curr[j] = max(prev[j], curr[j-1]);
        }
        swap(prev, curr);
    }
    cout << prev[n] << "\n";
    return 0;
}
```

---

## Edge Cases

| A | B | Output |
|---|---|---|
| `"ABC"` | `"ABC"` | `3` (identical) |
| `"ABC"` | `"DEF"` | `0` (no common characters) |
| `"A"` | `"A"` | `1` |
