# Problem 4 — Summer Array: Minimum Swaps

**Tier**: Easy (Q1) | **Marks**: 20 | **Topic**: Greedy / Inversion Count

> [!CAUTION]
> **Online Trap**: Most online solutions simulate bubble sort swaps — $O(N^2)$. This times out for $N = 10^5$. The correct approach is **inversion counting** in $O(N \log N)$.

---

## Problem

Given an array of $N$ distinct integers, find the **minimum number of adjacent swaps** required to sort the array in ascending order.

**Sample Input**:
```
arr = [3, 1, 2]
```
**Sample Output**:
```
2
```
**Explanation**: Swaps: `[3,1,2] → [1,3,2] → [1,2,3]` = 2 swaps.

**Constraints**: $1 \leq N \leq 10^5$, all elements distinct.

---

## Key Insight

> The minimum number of adjacent swaps to sort an array = the **number of inversions** in the array. An inversion is a pair $(i, j)$ where $i < j$ but $arr[i] > arr[j]$.

Count inversions using **Merge Sort** in $O(N \log N)$.

---

## Approach

Use merge sort. During the merge step, whenever an element from the right half is placed before an element from the left half, it contributes `(mid - left_ptr + 1)` inversions (all remaining left-half elements are larger).

**Complexity**: $O(N \log N)$ time, $O(N)$ auxiliary space.

---

## Python 3

```python
def count_inversions(arr):
    if len(arr) <= 1:
        return arr, 0

    mid = len(arr) // 2
    left, li = count_inversions(arr[:mid])
    right, ri = count_inversions(arr[mid:])

    merged, inversions = [], li + ri
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            merged.append(left[i]); i += 1
        else:
            merged.append(right[j]); j += 1
            inversions += len(left) - i  # all left[i:] are > right[j]
    merged.extend(left[i:]); merged.extend(right[j:])
    return merged, inversions

arr = list(map(int, input().split()))
_, ans = count_inversions(arr)
print(ans)
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;

long long merge_count(vector<int>& arr, int lo, int hi) {
    if (hi - lo <= 1) return 0;
    int mid = (lo + hi) / 2;
    long long inv = merge_count(arr, lo, mid) + merge_count(arr, mid, hi);
    vector<int> tmp;
    int i = lo, j = mid;
    while (i < mid && j < hi) {
        if (arr[i] <= arr[j]) { tmp.push_back(arr[i++]); }
        else { tmp.push_back(arr[j++]); inv += (mid - i); }
    }
    while (i < mid) tmp.push_back(arr[i++]);
    while (j < hi)  tmp.push_back(arr[j++]);
    copy(tmp.begin(), tmp.end(), arr.begin() + lo);
    return inv;
}

int main() {
    ios::sync_with_stdio(false); cin.tie(NULL);
    int n; cin >> n;
    vector<int> arr(n);
    for (int& x : arr) cin >> x;
    cout << merge_count(arr, 0, n) << "\n";
    return 0;
}
```

---

## Edge Cases

| Input | Output | Reason |
|---|---|---|
| `[1, 2, 3]` | `0` | Already sorted — 0 inversions |
| `[3, 2, 1]` | `3` | Fully reversed — 3 inversions |
| `[1]` | `0` | Single element |
