# Problem 1 — Maximum Subarray Sum

**Tier**: Easy (Q1) | **Marks**: 20 | **Topic**: Arrays

---

## Problem

Given an array of integers (which may include negative numbers), find the maximum sum of any **contiguous subarray**. The subarray must contain at least one element.

**Sample Input**:
```
arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
```
**Sample Output**:
```
6
```
**Explanation**: Subarray `[4, -1, 2, 1]` has sum = 6.

**Constraints**: $1 \leq N \leq 10^5$, $-10^4 \leq arr[i] \leq 10^4$.

---

## Key Insight

> Use **Kadane's Algorithm**: maintain a running sum `curr`. At each element, either extend the existing subarray or start fresh from the current element. Track the global maximum.

The decision at each step: `curr = max(arr[i], curr + arr[i])`.

---

## Approach

1. Initialize `curr = arr[0]`, `best = arr[0]`.
2. For each `arr[i]` from index 1 onward:
   - `curr = max(arr[i], curr + arr[i])` — extend or restart.
   - `best = max(best, curr)` — update global max.
3. Return `best`.

**Complexity**: $O(N)$ time, $O(1)$ space.

---

## Python 3

```python
def max_subarray_sum(arr):
    curr = best = arr[0]
    for x in arr[1:]:
        curr = max(x, curr + x)
        best = max(best, curr)
    return best

# --- Driver ---
arr = list(map(int, input().split()))
print(max_subarray_sum(arr))
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);

    int n; cin >> n;
    vector<int> arr(n);
    for (int& x : arr) cin >> x;

    long long curr = arr[0], best = arr[0];
    for (int i = 1; i < n; i++) {
        curr = max((long long)arr[i], curr + arr[i]);
        best = max(best, curr);
    }
    cout << best << "\n";
    return 0;
}
```

---

## Edge Cases

| Input | Output | Reason |
|---|---|---|
| `[-5]` | `-5` | Single element |
| `[-3, -1, -4]` | `-1` | All negative — return least negative |
| `[0, 0, 0]` | `0` | All zeros |
