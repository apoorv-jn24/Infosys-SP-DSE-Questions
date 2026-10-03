# Problem 15 — Packing Gifts into K Boxes

**Tier**: Hard (Q3) | **Marks**: 50 | **Topic**: Binary Search on Answer / Contiguous Partitioning

---

## Problem

You have $N$ gifts in a conveyor line with weights $w_1, w_2, \ldots, w_N$ arriving in order. You must distribute all gifts into **$K$ contiguous boxes** without reordering them. The **weight of a box** is the sum of weights of the gifts placed inside it. Find the assignment that **minimizes the maximum box weight**.

**Sample Input**:
```
5 3
3 5 8 7 4
```
**Sample Output**:
```
11
```
**Explanation**:
The optimal partition into 3 contiguous segments is:
- Box 1: `[3, 5]` (sum = 8)
- Box 2: `[8]` (sum = 8)
- Box 3: `[7, 4]` (sum = 11)
The maximum box weight is $\max(8, 8, 11) = 11$. Any other 3-partition has a box of weight $\geq 11$.

**Constraints**: $1 \leq K \leq N \leq 10^5$, $1 \leq w_i \leq 10^9$.

---

## Key Insight

> **Monotonicity & Binary Search on the Answer**:
> If a capacity $C$ can accommodate all gifts in $\leq K$ boxes, any capacity $C' > C$ can as well.
> 1. Lower bound: $\text{lo} = \max(w_i)$ (every individual gift must fit into a box).
> 2. Upper bound: $\text{hi} = \sum w_i$ (all gifts fit into 1 box).
> 3. Feasibility check: Greedily pack gifts in the given sequence into the current box. As soon as adding the next gift exceeds capacity $C$, close the current box and start a new one. If total boxes $\leq K$, capacity $C$ is feasible.

---

## Approach

1. `lo = max(weights)`, `hi = sum(weights)`.
2. While `lo < hi`:
   - `mid = (lo + hi) // 2`.
   - If `can_pack(weights, K, mid)`: `hi = mid`.
   - Else: `lo = mid + 1`.
3. Return `lo`.

**Complexity**: $O(N \log(\sum w))$ time, $O(1)$ auxiliary space.

---

## Python 3

```python
def can_pack(weights, K, max_sum):
    boxes = 1
    current = 0
    for w in weights:
        if w > max_sum:
            return False
        if current + w > max_sum:
            boxes += 1
            current = 0
        current += w
    return boxes <= K

def min_max_cost(weights, K):
    lo, hi = max(weights), sum(weights)
    while lo < hi:
        mid = (lo + hi) // 2
        if can_pack(weights, K, mid):
            hi = mid
        else:
            lo = mid + 1
    return lo

import sys
lines = sys.stdin.read().split()
if lines:
    n, K = int(lines[0]), int(lines[1])
    weights = list(map(int, lines[2:2+n]))
    print(min_max_cost(weights, K))
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

bool can_pack(const vector<ll>& w, int K, ll lim) {
    int boxes = 1; ll cur = 0;
    for (ll x : w) {
        if (x > lim) return false;
        if (cur + x > lim) {
            boxes++;
            cur = 0;
        }
        cur += x;
    }
    return boxes <= K;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);

    int n, K;
    if (!(cin >> n >> K)) return 0;

    vector<ll> w(n);
    for (ll& x : w) cin >> x;

    ll lo = *max_element(w.begin(), w.end());
    ll hi = accumulate(w.begin(), w.end(), 0LL);

    while (lo < hi) {
        ll mid = lo + (hi - lo) / 2;
        if (can_pack(w, K, mid)) {
            hi = mid;
        } else {
            lo = mid + 1;
        }
    }

    cout << lo << "\n";
    return 0;
}
```

---

## Edge Cases

| Scenario | Input | K | Output | Reason |
|---|---|---|---|---|
| Single box | `[3, 5, 8]` | 1 | `16` | Sum of all elements |
| K equals N | `[3, 5, 8]` | 3 | `8` | Max element |
| Identical weights | `[4, 4, 4, 4]` | 2 | `8` | Two boxes of 8 each |
