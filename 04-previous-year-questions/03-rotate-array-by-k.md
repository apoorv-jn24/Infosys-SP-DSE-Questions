# Problem 3 — Rotate Array by K Positions

**Tier**: Easy (Q1) | **Marks**: 20 | **Topic**: Arrays / Reversal

---

## Problem

Given an array of $N$ integers, rotate it **to the right by $K$ positions** in-place using $O(1)$ extra space.

**Sample Input**:
```
arr = [1, 2, 3, 4, 5, 6, 7]
K = 3
```
**Sample Output**:
```
[5, 6, 7, 1, 2, 3, 4]
```

**Constraints**: $1 \leq N \leq 10^5$, $0 \leq K \leq 10^9$.

---

## Key Insight

> **Three reversals**: Normalize $K = K \bmod N$. Then:
> 1. Reverse the whole array.
> 2. Reverse the first $K$ elements.
> 3. Reverse the remaining $N - K$ elements.

No extra array needed — all in $O(1)$ space.

---

## Approach

1. `K = K % N` — handles $K > N$.
2. `reverse(arr, 0, N-1)` — full array.
3. `reverse(arr, 0, K-1)` — first K elements.
4. `reverse(arr, K, N-1)` — remaining elements.

**Complexity**: $O(N)$ time, $O(1)$ space.

---

## Python 3

```python
def rotate(arr, k):
    n = len(arr)
    k %= n
    if k == 0:
        return arr

    def rev(lo, hi):
        while lo < hi:
            arr[lo], arr[hi] = arr[hi], arr[lo]
            lo += 1; hi -= 1

    rev(0, n - 1)
    rev(0, k - 1)
    rev(k, n - 1)
    return arr

# --- Driver ---
arr = list(map(int, input().split()))
k = int(input())
print(*rotate(arr, k))
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);

    int n, k; cin >> n >> k;
    vector<int> arr(n);
    for (int& x : arr) cin >> x;

    k %= n;
    reverse(arr.begin(), arr.end());
    reverse(arr.begin(), arr.begin() + k);
    reverse(arr.begin() + k, arr.end());

    for (int i = 0; i < n; i++)
        cout << arr[i] << " \n"[i == n-1];
    return 0;
}
```

---

## Edge Cases

| Input | K | Output | Reason |
|---|---|---|---|
| `[1,2,3,4,5]` | 0 | `[1,2,3,4,5]` | No rotation |
| `[1,2,3,4,5]` | 5 | `[1,2,3,4,5]` | Full rotation = identity |
| `[1,2,3,4,5]` | 7 | `[4,5,1,2,3]` | K > N, use K % N = 2 |
