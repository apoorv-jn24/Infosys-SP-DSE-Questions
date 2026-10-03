# Problem 12 — Maximum XOR-Sum in Range [0, K]

**Tier**: Medium (Q2) | **Marks**: 30 | **Topic**: Bit Manipulation / Linear XOR Basis

---

## Problem

Given an array of non-negative integers and an integer $K$, find the **maximum XOR of any subset** of the array such that the XOR sum is **at most $K$**.

**Sample Input**:
```
5 7
3 5 6 8 10
```
**Sample Output**:
```
7
```
**Explanation**: Subset `[5, 6]` has XOR $= 5 \oplus 6 = 3 \leq 7$. Subset `[3, 5, 6]` has XOR $= 3 \oplus 5 \oplus 6 = 0 \leq 7$. The subset with maximum XOR $\leq 7$ is `[3, 5, 6]` with basis combinations reaching $7$ (e.g., $10 \oplus 8 \oplus 5 = 7 \leq 7$).

**Constraints**: $1 \leq N \leq 10^5$, $0 \leq arr[i] \leq 10^9$, $0 \leq K \leq 10^9$.

---

## Key Insight

> 1. Construct a **linear XOR basis** over GF(2).
> 2. Perform **Gauss-Jordan elimination** to convert the basis into **Reduced Row Echelon Form (RREF)**: for every pivot bit $i$, clear bit $i$ from all higher basis vectors $j > i$.
> 3. In RREF, each basis vector's pivot bit is unique to that vector. Greedily considering basis vectors from highest pivot bit to lowest allows setting bits without perturbing higher-order decisions.
> 4. If `(result ^ basis[b]) <= K`, greedily apply `result ^= basis[b]`.

---

## Approach

1. Initialize `basis = [0] * 60`.
2. Insert each array element $x$ into the basis from bit 59 down to 0:
   - If bit $b$ is set in $x$: if `basis[b] == 0`, set `basis[b] = x` and break; else `x ^= basis[b]`.
3. Apply Gauss-Jordan reduction: for each pivot $i$, if `basis[i]` exists, XOR `basis[i]` into any higher row `j > i` that has bit $i$ set.
4. Iterate from bit 59 down to 0: if `basis[b]` is present and `(result ^ basis[b]) <= K`, toggle `result ^= basis[b]`.
5. Return `result`.

**Complexity**: $O(N \log(\max A) + \log^2(\max A))$ time, $O(\log(\max A))$ space.

---

## Python 3

```python
def max_xor_leq_k(arr, K, bits=60):
    basis = [0] * bits
    for x in arr:
        for b in reversed(range(bits)):
            if not (x >> b) & 1:
                continue
            if not basis[b]:
                basis[b] = x
                break
            x ^= basis[b]

    # Gauss-Jordan: convert to Reduced Row Echelon Form
    for i in range(bits):
        if basis[i]:
            for j in range(i + 1, bits):
                if (basis[j] >> i) & 1:
                    basis[j] ^= basis[i]

    # Greedily construct max XOR <= K from MSB to LSB
    result = 0
    for b in reversed(range(bits)):
        if basis[b] and (result ^ basis[b]) <= K:
            result ^= basis[b]
    return result

import sys
lines = sys.stdin.read().split()
if lines:
    n, K = int(lines[0]), int(lines[1])
    arr = list(map(int, lines[2:2+n]))
    print(max_xor_leq_k(arr, K))
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);

    int n; ll K;
    if (!(cin >> n >> K)) return 0;

    const int BITS = 60;
    vector<ll> basis(BITS, 0);

    for (int i = 0; i < n; i++) {
        ll x; cin >> x;
        for (int b = BITS - 1; b >= 0 && x; b--) {
            if (!((x >> b) & 1)) continue;
            if (!basis[b]) {
                basis[b] = x;
                break;
            }
            x ^= basis[b];
        }
    }

    // Gauss-Jordan: Reduced Row Echelon Form
    for (int i = 0; i < BITS; i++) {
        if (basis[i]) {
            for (int j = i + 1; j < BITS; j++) {
                if ((basis[j] >> i) & 1) {
                    basis[j] ^= basis[i];
                }
            }
        }
    }

    ll result = 0;
    for (int b = BITS - 1; b >= 0; b--) {
        if (basis[b] && (result ^ basis[b]) <= K) {
            result ^= basis[b];
        }
    }

    cout << result << "\n";
    return 0;
}
```

---

## Edge Cases

| Scenario | Input | K | Output | Reason |
|---|---|---|---|---|
| All zeros | `[0]` | 5 | `0` | Zero XOR |
| Element equals K | `[7]` | 7 | `7` | Exact match |
| Element exceeds K | `[8]` | 7 | `0` | 8 > 7 cannot be used |
| Bit cancelation | `[6, 5]` | 5 | `5` | Single element 5 reaches bound |
