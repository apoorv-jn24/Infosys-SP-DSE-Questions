# Problem 8 — Minimum Ugliness of Binary String

**Tier**: Medium (Q2) | **Marks**: 30 | **Topic**: Greedy with Regret / Run-Length Encoding

---

## Problem

Given a binary string $S$ of length $N$ and an integer $K$, you can flip **at most $K$ characters anywhere** in the string (0→1 or 1→0). The **ugliness** of a string is the number of adjacent pairs where the two characters differ (i.e., the number of transitions between blocks of identical characters). Find the **minimum possible ugliness** achievable after at most $K$ flips.

**Sample Input**:
```
010101
1
```
**Sample Output**:
```
3
```
**Explanation**: Flipping the second character (`010101` → `000101`) eliminates 2 transitions (at indices 0–1 and 1–2). The ugliness drops from 5 to 3.

**Constraints**: $1 \leq N \leq 10^5$, $0 \leq K \leq N$.

---

## Key Insight

> 1. Compress $S$ into runs of consecutive identical characters with lengths $L_1, L_2, \ldots, L_m$.
> 2. The initial ugliness is $m - 1$ (the number of boundaries between adjacent runs).
> 3. If we flip an **interior run** of length $L_i$ ($1 < i < m$) completely, it merges its left and right neighbors (which have the same character), eliminating **2 boundaries** at the cost of $L_i$ flips.
> 4. If we flip the **first run** ($i = 1$) or the **last run** ($i = m$), it eliminates **1 boundary** at cost $L_1$ or $L_m$.
> 5. Flipping two adjacent runs merges them into each other rather than eliminating 2 boundaries each. Hence, chosen interior runs to flip must be **pairwise non-adjacent**.
> 6. Finding the minimum cost to pick $t$ non-adjacent runs from an array is solved optimally using a **priority queue with regret** (the dual update $v_l + v_r - v_i$).

---

## Approach

1. Compute run lengths $runs = [L_1, \ldots, L_m]$. If $m \leq 1$, return 0.
2. Consider 4 cases for whether we flip the first run, the last run, both, or neither:
   - Deduct the cost of flipping boundary runs from $K$.
   - On the remaining interior runs, compute $f[t]$ = minimum cost to flip $t$ pairwise non-adjacent runs using a regret heap.
   - Use binary search (`bisect_right` / `upper_bound`) on $f$ to find the maximum $t$ affordable with the remaining flip budget.
   - Reduction in ugliness = $(\text{boundary flips}) + 2 \times t$.
3. Return initial ugliness minus the maximum reduction.

**Complexity**: $O(m \log m)$ time, $O(m)$ space.

---

## Python 3

```python
import itertools
import heapq
from bisect import bisect_right

def min_cost_non_adjacent(costs):
    """Computes minimum cost to pick t pairwise non-adjacent elements using a regret-greedy heap."""
    n = len(costs)
    INF = float("inf")
    val = [INF] + list(costs) + [INF]
    left = list(range(-1, n + 1))
    right = list(range(1, n + 3))
    alive = [True] * (n + 2)
    heap = [(val[i], i) for i in range(1, n + 1)]
    heapq.heapify(heap)

    f = [0]
    total = 0
    while heap:
        v, i = heapq.heappop(heap)
        if not alive[i] or v != val[i] or v >= INF:
            continue
        total += v
        f.append(total)
        l, r = left[i], right[i]
        val[i] = val[l] + val[r] - val[i]  # Regret node
        alive[l] = alive[r] = False
        left[i], right[i] = left[l], right[r]
        if left[i] >= 0:
            right[left[i]] = i
        if right[i] <= n + 1:
            left[right[i]] = i
        heapq.heappush(heap, (val[i], i))
    return f

def min_ugliness(S, K):
    runs = [len(list(g)) for _, g in itertools.groupby(S)]
    m = len(runs)
    if m <= 1:
        return 0

    best_gain = 0
    for take_first in (0, 1):
        for take_last in (0, 1):
            if m == 2 and take_first and take_last:
                continue
            cost = take_first * runs[0] + take_last * runs[-1]
            if cost > K:
                continue
            inner = runs[1 + take_first : m - 1 - take_last]
            f = min_cost_non_adjacent(inner)
            t = bisect_right(f, K - cost) - 1
            best_gain = max(best_gain, take_first + take_last + 2 * t)

    return (m - 1) - best_gain

S = input().strip()
K = int(input().strip())
print(min_ugliness(S, K))
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);

    string S; ll K;
    if (!(cin >> S >> K)) return 0;

    vector<ll> runs;
    for (size_t i = 0; i < S.size();) {
        size_t j = i;
        while (j < S.size() && S[j] == S[i]) j++;
        runs.push_back(j - i);
        i = j;
    }

    int m = runs.size();
    if (m <= 1) { cout << 0 << "\n"; return 0; }

    auto minCostNonAdjacent = [](const vector<ll>& costs) {
        int n = costs.size();
        const ll INF = LLONG_MAX / 4;
        vector<ll> val(n + 2, INF);
        for (int i = 0; i < n; i++) val[i + 1] = costs[i];
        vector<int> L(n + 2), R(n + 2);
        for (int i = 0; i < n + 2; i++) { L[i] = i - 1; R[i] = i + 1; }
        vector<char> alive(n + 2, 1);
        priority_queue<pair<ll,int>, vector<pair<ll,int>>, greater<pair<ll,int>>> pq;
        for (int i = 1; i <= n; i++) pq.push({val[i], i});
        vector<ll> f(1, 0); ll total = 0;
        while (!pq.empty()) {
            auto top = pq.top(); pq.pop();
            ll v = top.first; int i = top.second;
            if (!alive[i] || v != val[i] || v >= INF) continue;
            total += v; f.push_back(total);
            int l = L[i], r = R[i];
            ll nv = val[l] + val[r] - val[i];
            val[i] = min(nv, INF);
            alive[l] = alive[r] = 0;
            L[i] = (l >= 0) ? L[l] : -1;
            R[i] = (r <= n + 1) ? R[r] : n + 2;
            if (L[i] >= 0) R[L[i]] = i;
            if (R[i] <= n + 1) L[R[i]] = i;
            pq.push({val[i], i});
        }
        return f;
    };

    int bestGain = 0;
    for (int tf = 0; tf <= 1; tf++) {
        for (int tl = 0; tl <= 1; tl++) {
            if (m == 2 && tf && tl) continue;
            ll cost = tf * runs[0] + tl * runs[m - 1];
            if (cost > K) continue;
            int lo = 1 + tf, hi = m - 1 - tl;
            vector<ll> inner;
            for (int i = lo; i < hi; i++) inner.push_back(runs[i]);
            vector<ll> f = minCostNonAdjacent(inner);
            int t = int(upper_bound(f.begin(), f.end(), K - cost) - f.begin()) - 1;
            bestGain = max(bestGain, tf + tl + 2 * t);
        }
    }

    cout << (m - 1) - bestGain << "\n";
    return 0;
}
```

---

## Edge Cases

| Input | K | Output | Reason |
|---|---|---|---|
| `"0000"` | 2 | `0` | Already single block; 0 ugliness |
| `"0101"` | 4 | `0` | Flip all to single value |
| `"01"` | 1 | `0` | Flip one char to match other |
| `"010101"` | 1 | `3` | Flip interior run of length 1 |
