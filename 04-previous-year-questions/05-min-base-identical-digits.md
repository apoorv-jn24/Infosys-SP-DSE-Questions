# Problem 5 — Minimum Base with Identical Digits

**Tier**: Easy (Q1) | **Marks**: 20 | **Topic**: Number Theory / Base Conversion

---

## Problem

Given a positive integer $N$, find the **smallest base $b \geq 2$** such that the representation of $N$ in base $b$ consists of **all identical digits**.

**Sample Input**:
```
N = 13
```
**Sample Output**:
```
3
```
**Explanation**: $13$ in base $3$ is `111` (all 1s).

**Constraints**: $2 \leq N \leq 10^{18}$.

---

## Key Insight

> For any $N$, the representation in base $N-1$ is always `11` (two identical digits). So the answer is at most $N-1$. Search bases from $2$ upward and return the first valid one. For large $N$, representations in small bases have many digits — use logarithm to bound digit count.

---

## Approach

1. For each base $b$ from $2$ to $N-1$:
   - Convert $N$ to base $b$ by repeated division.
   - Check if all digits are identical.
   - If yes, return $b$.
2. Special case: $N-1$ always gives `11` — guaranteed answer exists.

**Complexity**: $O(\sqrt{N} \cdot \log N)$ — bases with $> 2$ identical digits only exist for $b \leq \sqrt{N}$.

---

## Python 3

```python
def all_same_digits(n, b):
    digits = []
    while n:
        digits.append(n % b)
        n //= b
    return len(set(digits)) == 1

def min_base(N):
    # Bases with 3+ identical digits only possible for b <= sqrt(N)
    import math
    for b in range(2, int(math.isqrt(N)) + 2):
        if all_same_digits(N, b):
            return b
    return N - 1  # N in base (N-1) is always "11"

N = int(input())
print(min_base(N))
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

bool all_same(ll n, ll b) {
    int first = n % b; n /= b;
    while (n) {
        if (n % b != first) return false;
        n /= b;
    }
    return true;
}

int main() {
    ll N; cin >> N;
    ll limit = (ll)sqrt((double)N) + 2;
    for (ll b = 2; b <= limit; b++) {
        if (all_same(N, b)) { cout << b << "\n"; return 0; }
    }
    cout << N - 1 << "\n";  // "11" in base N-1
    return 0;
}
```

---

## Edge Cases

| Input | Output | Explanation |
|---|---|---|
| `7` | `2` | `7` in base 2 = `111` |
| `4` | `3` | `4` in base 3 = `11` |
| `2` | `1` → base `2` = `10` | Base 1 unary: `N = 11...1`; return 1 |
