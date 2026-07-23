# Problem 18 — Longest Bitwise-Compatible LIS

**Tier**: Hard (Q3) | **Marks**: 50 | **Topic**: Bit Manipulation + LIS

> [!CAUTION]
> **Online Trap**: Online solutions run a standard LIS on raw values, completely ignoring the "bitwise compatibility" condition. This produces a wrong answer. The condition must be decoded to **strictly increasing MSB (Most Significant Bit) indices**.

---

## Problem

Given an array of $N$ positive integers, find the length of the longest subsequence such that for any two consecutive elements $a$ and $b$ in the subsequence, the **most significant bit of $b$ is strictly greater** than the most significant bit of $a$. (i.e., $\lfloor \log_2 b \rfloor > \lfloor \log_2 a \rfloor$).

**Sample Input**:
```
arr = [1, 3, 5, 2, 8, 4, 16]
```
**Sample Output**:
```
4
```
**Explanation**: MSBs: 1→0, 3→1, 5→2, 2→1, 8→3, 4→2, 16→4. Longest strictly increasing MSB sequence: 0→1→2→3 (e.g., 1→3→5→8), length = 4.

**Constraints**: $1 \leq N \leq 10^5$, $1 \leq arr[i] \leq 10^9$.

---

## Key Insight

> **Transform each element to its MSB index**, then run **standard LIS on MSB indices** in $O(N \log N)$ using patience sorting.

`msb(x) = x.bit_length() - 1`  (Python) or `31 - __builtin_clz(x)` (C++)

Since we want strictly increasing MSB indices, this is exactly LIS on the transformed array.

---

## Approach

1. Transform: `msb_arr[i] = arr[i].bit_length() - 1`.
2. Run $O(N \log N)$ patience sorting LIS on `msb_arr`.
3. Return LIS length.

**Complexity**: $O(N \log N)$ time, $O(N)$ space.

---

## Python 3

```python
from bisect import bisect_left

def lis_length(seq):
    tails = []
    for x in seq:
        pos = bisect_left(tails, x)
        if pos == len(tails):
            tails.append(x)
        else:
            tails[pos] = x
    return len(tails)

def longest_bitwise_lis(arr):
    msb_arr = [x.bit_length() - 1 for x in arr]
    return lis_length(msb_arr)

arr = list(map(int, input().split()))
print(longest_bitwise_lis(arr))
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false); cin.tie(NULL);
    int n; cin >> n;
    vector<int> arr(n);
    for (int& x : arr) cin >> x;

    // Transform to MSB indices
    vector<int> msb(n);
    for (int i = 0; i < n; i++)
        msb[i] = 31 - __builtin_clz(arr[i]);  // MSB position

    // LIS via patience sorting
    vector<int> tails;
    for (int x : msb) {
        auto it = lower_bound(tails.begin(), tails.end(), x);
        if (it == tails.end()) tails.push_back(x);
        else *it = x;
    }
    cout << tails.size() << "\n";
    return 0;
}
```

---

## Why Online Solutions Fail

Running standard LIS on raw values like `[1, 3, 5, 2, 8, 4, 16]` gives LIS = 4 (e.g., 1→3→5→8 or 1→3→4→16) — this happens to agree for this sample but fails on:

`arr = [5, 6, 7]` — raw LIS = 3, but MSBs are all `2` → bitwise LIS = 1. Online solutions return 3 (wrong).
