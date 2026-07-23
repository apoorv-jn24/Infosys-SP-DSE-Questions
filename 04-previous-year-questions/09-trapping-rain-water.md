# Problem 9 — Trapping Rain Water

**Tier**: Medium (Q2) | **Marks**: 30 | **Topic**: Two Pointers / Prefix Max

---

## Problem

Given an array of $N$ non-negative integers representing the height of bars in a histogram (each bar has width 1), compute how much **water can be trapped** after it rains.

**Sample Input**:
```
height = [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]
```
**Sample Output**:
```
6
```

**Constraints**: $1 \leq N \leq 2 \times 10^4$, $0 \leq height[i] \leq 10^5$.

---

## Key Insight

> Water at position $i$ = `min(max_left[i], max_right[i]) - height[i]`. Use **two pointers** (left and right converging) to compute this in $O(1)$ space without prefix arrays.

---

## Approach (Two Pointers — $O(1)$ space)

1. `lo = 0`, `hi = N-1`, `left_max = right_max = 0`, `water = 0`.
2. While `lo <= hi`:
   - If `height[lo] <= height[hi]`: process left side.
     - If `height[lo] >= left_max`: update `left_max`.
     - Else: `water += left_max - height[lo]`.
     - `lo++`.
   - Else: process right side symmetrically. `hi--`.
3. Return `water`.

**Complexity**: $O(N)$ time, $O(1)$ space.

---

## Python 3

```python
def trap(height):
    lo, hi = 0, len(height) - 1
    left_max = right_max = water = 0
    while lo <= hi:
        if height[lo] <= height[hi]:
            if height[lo] >= left_max:
                left_max = height[lo]
            else:
                water += left_max - height[lo]
            lo += 1
        else:
            if height[hi] >= right_max:
                right_max = height[hi]
            else:
                water += right_max - height[hi]
            hi -= 1
    return water

height = list(map(int, input().split()))
print(trap(height))
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false); cin.tie(NULL);
    int n; cin >> n;
    vector<int> h(n);
    for (int& x : h) cin >> x;

    int lo = 0, hi = n-1, lmax = 0, rmax = 0;
    long long water = 0;
    while (lo <= hi) {
        if (h[lo] <= h[hi]) {
            lmax = max(lmax, h[lo]);
            water += lmax - h[lo];
            lo++;
        } else {
            rmax = max(rmax, h[hi]);
            water += rmax - h[hi];
            hi--;
        }
    }
    cout << water << "\n";
    return 0;
}
```

---

## Edge Cases

| Input | Output |
|---|---|
| `[3, 0, 3]` | `3` |
| `[1, 2, 3]` | `0` (monotone increasing — no trap) |
| `[3, 2, 1]` | `0` (monotone decreasing) |
| `[1]` | `0` |
