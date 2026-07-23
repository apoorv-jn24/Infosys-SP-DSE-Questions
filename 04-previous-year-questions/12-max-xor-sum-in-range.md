# Problem 12 — Maximum XOR-Sum in Range [0, K]

**Tier**: Medium (Q2) | **Marks**: 30 | **Topic**: Bit Manipulation / Greedy

---

## Problem

Given an array of non-negative integers and an integer $K$, find the **maximum XOR of any subset** of the array such that the XOR value is **at most $K$**.

**Sample Input**:
```
arr = [3, 5, 6, 8, 10]
K = 7
```
**Sample Output**:
```
7
```
**Explanation**: XOR of `3 ^ 4`... *(adjust to match actual problem constraint)*.

**Constraints**: $1 \leq N \leq 10^5$, $0 \leq arr[i] \leq 10^9$, $0 \leq K \leq 10^9$.

---

## Key Insight

> Build a **linear basis (Gaussian Elimination over GF(2))** from the array. Then greedily construct the maximum XOR ≤ K by deciding bit-by-bit from the most significant bit whether to set it, checking feasibility against K.

---

## Approach

1. Build XOR basis from all array elements.
2. Start with `result = 0`.
3. For each bit from high to low:
   - If setting this bit (`result ^ basis[bit]`) still keeps result ≤ K, set it.
4. Return `result`.

**Complexity**: $O(N \log(\max A))$ for basis construction, $O(\log^2 K)$ for greedy query.

---

## Python 3

```python
def max_xor_leq_k(arr, K):
    # Build linear basis
    basis = []
    for x in arr:
        cur = x
        for b in basis:
            cur = min(cur, cur ^ b)
        if cur:
            basis.append(cur)
            basis.sort(reverse=True)

    # Greedy: build max XOR <= K
    result = 0
    for b in basis:
        if (result ^ b) <= K:
            result ^= b
    return result

arr = list(map(int, input().split()))
K = int(input())
print(max_xor_leq_k(arr, K))
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false); cin.tie(NULL);
    int n; long long K; cin >> n >> K;
    vector<long long> arr(n);
    for (auto& x : arr) cin >> x;

    // Build basis
    vector<long long> basis;
    for (long long x : arr) {
        for (long long b : basis) x = min(x, x ^ b);
        if (x) { basis.push_back(x); sort(basis.rbegin(), basis.rend()); }
    }

    long long result = 0;
    for (long long b : basis)
        if ((result ^ b) <= K) result ^= b;

    cout << result << "\n";
    return 0;
}
```

---

## Edge Cases

| Scenario | Output |
|---|---|
| `arr = [0]`, K = 5 | `0` |
| `arr = [7]`, K = 7 | `7` |
| `arr = [8]`, K = 7 | `0` (8 > K, can't use it) |
