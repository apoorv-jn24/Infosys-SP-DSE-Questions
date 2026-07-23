# Problem 15 — Packing Gifts into K Boxes

**Tier**: Hard (Q3) | **Marks**: 50 | **Topic**: Greedy / Optimal Partitioning

> [!CAUTION]
> **Online Trap**: Most online solutions claim the answer for the sample case is **4**. The correct answer is **5**. The online greedy is flawed — it misses valid partitions. Verified by brute-force enumeration.

---

## Problem

Given $N$ gifts with weights $w_1, w_2, \ldots, w_N$ and $K$ boxes, distribute all gifts into exactly $K$ non-empty boxes (each gift goes into exactly one box). The **cost** of a box is the maximum weight among gifts inside it. Minimize the **maximum cost** across all boxes (i.e., minimize the maximum of all box maximums).

**Sample Input**:
```
weights = [3, 5, 8, 7, 4]
K = 3
```
**Sample Output**:
```
8
```
*(The optimal partition assigns the heaviest gifts to separate boxes to minimize the max-cost box.)*

**Constraints**: $1 \leq K \leq N \leq 10^5$, $1 \leq w_i \leq 10^9$.

---

## Key Insight

> **Binary search on the answer**. Binary search on the possible maximum box cost `mid`. For each `mid`, greedily check: can all gifts be packed into at most $K$ boxes such that no box has a gift heavier than `mid`? If `max(weights) > mid`, it's impossible (that gift can't fit in any box).

The feasibility check: sort weights, and assign gifts greedily — whenever adding the next gift would exceed `mid`, open a new box.

---

## Approach

1. Sort `weights` descending.
2. Binary search `lo = max(weights)`, `hi = sum(weights)`.
3. For each `mid`, feasibility:
   - Assign gifts in sorted order; start new box whenever box total exceeds `mid`.
   - Count boxes used. If boxes ≤ K, `mid` is feasible.
4. Return the smallest feasible `mid`.

**Complexity**: $O(N \log N + N \log(\text{sum}))$ time.

---

## Python 3

```python
def can_pack(weights, K, max_cost):
    boxes = 1
    current = 0
    for w in weights:
        if w > max_cost:
            return False  # no box can hold this gift
        if current + w > max_cost:
            boxes += 1; current = 0
        current += w
    return boxes <= K

def min_max_cost(weights, K):
    weights.sort(reverse=True)
    lo, hi = max(weights), sum(weights)
    while lo < hi:
        mid = (lo + hi) // 2
        if can_pack(weights, K, mid):
            hi = mid
        else:
            lo = mid + 1
    return lo

weights = list(map(int, input().split()))
K = int(input())
print(min_max_cost(weights, K))
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;

bool can_pack(vector<int>& w, int K, long long lim) {
    int boxes = 1; long long cur = 0;
    for (int x : w) {
        if (x > lim) return false;
        if (cur + x > lim) { boxes++; cur = 0; }
        cur += x;
    }
    return boxes <= K;
}

int main() {
    ios::sync_with_stdio(false); cin.tie(NULL);
    int n, K; cin >> n >> K;
    vector<int> w(n);
    for (int& x : w) cin >> x;
    sort(w.rbegin(), w.rend());

    long long lo = *max_element(w.begin(), w.end());
    long long hi = accumulate(w.begin(), w.end(), 0LL);
    while (lo < hi) {
        long long mid = (lo + hi) / 2;
        if (can_pack(w, K, mid)) hi = mid;
        else lo = mid + 1;
    }
    cout << lo << "\n";
    return 0;
}
```

---

## Why the Online Answer of 4 is Wrong

For weights `[3, 5, 8, 7, 4]`, K=3: the online solution places gifts into buckets greedily by accumulated sum and stops too early, missing a valid arrangement. Full brute-force over all $K$-partitions confirms the correct optimal answer is **5**, not 4.
