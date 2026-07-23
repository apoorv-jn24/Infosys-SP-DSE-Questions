# Problem 17 — Maximum XOR of Half-Sized Subset

**Tier**: Hard (Q3) | **Marks**: 50 | **Topic**: Bit Manipulation / Gaussian Elimination

---

## Problem

Given an array of $N$ integers ($N$ even), choose exactly $N/2$ elements to form a subset. Find the **maximum possible XOR** of all elements in the chosen subset.

**Sample Input**:
```
arr = [3, 5, 6, 8, 10, 12]   (N=6, choose 3)
```
**Sample Output**:
```
15
```

**Constraints**: $2 \leq N \leq 50$ (even), $1 \leq arr[i] \leq 10^9$.

---

## Key Insight

> Build a **linear XOR basis** (Gaussian Elimination over GF(2)) from the array. The maximum XOR of any subset (regardless of size) is obtained by greedily activating basis vectors from highest bit to lowest. For the size constraint ($N/2$ elements), the key insight is: if we can achieve max XOR from any subset, the $N/2$ size constraint can usually be satisfied by adding "neutral" XOR pairs (elements that XOR to 0) to balance parity — but this depends on whether the basis spans a space including size-parity.

For small $N$ (≤ 50), an alternative is bitmask DP over subsets of size $N/2$.

---

## Approach (Bitmask for N ≤ 20, Basis for N ≤ 50)

For $N \leq 20$: enumerate all $\binom{N}{N/2}$ subsets and track max XOR.

For $N \leq 50$: Gaussian Elimination basis + greedy.

---

## Python 3

```python
from itertools import combinations

def max_xor_half_subset(arr):
    n = len(arr)
    half = n // 2
    best = 0
    for subset in combinations(arr, half):
        xor_val = 0
        for x in subset: xor_val ^= x
        best = max(best, xor_val)
    return best

arr = list(map(int, input().split()))
print(max_xor_half_subset(arr))
```

## C++ 17 (Bitmask for small N)

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false); cin.tie(NULL);
    int n; cin >> n;
    vector<int> arr(n);
    for (int& x : arr) cin >> x;

    int half = n / 2;
    long long best = 0;

    // Enumerate all subsets of size n/2
    for (int mask = 0; mask < (1 << n); mask++) {
        if (__builtin_popcount(mask) != half) continue;
        long long xorv = 0;
        for (int i = 0; i < n; i++)
            if (mask >> i & 1) xorv ^= arr[i];
        best = max(best, xorv);
    }
    cout << best << "\n";
    return 0;
}
```

---

## Non-Negotiable Prerequisite

XOR properties used here:
- `a ^ a = 0` (self-cancellation)
- `a ^ 0 = a` (identity)
- XOR is commutative and associative

Know MSB: `msb(x) = x.bit_length() - 1` in Python, `31 - __builtin_clz(x)` in C++.
