# Problem 5 — Minimum Base with Identical Digits

**Tier**: Easy (Q1) | **Marks**: 20 | **Topic**: Number Theory / Base Conversion

---

## Problem

Given a positive integer $N \geq 3$, find the **smallest base $b \geq 2$** such that the representation of $N$ in base $b$ consists of **all identical digits** with at least two digits (i.e., $2 \leq b \leq N-1$).

**Sample Input**:
```
N = 13
```
**Sample Output**:
```
3
```
**Explanation**: $13$ in base $3$ is `111` (three identical digits '1').

**Constraints**: $3 \leq N \leq 10^{12}$.

---

## Key Insight

> In base $b$, $N$ can have either:
> 1. **$\geq 3$ digits**: Here $b^2 \leq N$, which means $b \leq \sqrt{N}$. We can iterate $b$ from $2$ up to $\lfloor\sqrt{N}\rfloor$ and test if all digits match.
> 2. **Exactly 2 digits ("dd")**: $N = d \cdot b + d = d \cdot (b + 1)$ where $1 \leq d < b$.
>    Thus, $d$ must be a divisor of $N$, and $b = N/d - 1$.
>    To minimize $b$, we want to maximize the divisor $d$ such that $d < b \iff d < N/d - 1 \iff d(d+1) < N$.
>    Since $d < b$, we only need to search divisors $d \leq \lfloor\sqrt{N}\rfloor$.
>    Notice $d = 1$ always works: $b = N - 1$ gives `"11"`.

---

## Approach

1. For each base $b$ from $2$ to $\lfloor\sqrt{N}\rfloor + 1$:
   - Check if $N$ in base $b$ has all identical digits. If yes, return $b$.
2. To check 2-digit cases $N = d(b+1)$, loop $d$ from $\lfloor\sqrt{N}\rfloor$ down to $1$:
   - If $d$ divides $N$:
     - Let $b = N // d - 1$.
     - If $d < b$ and $b \geq 2$, return $b$.
3. Fallback: $N - 1$ (always yields `11` in base $N-1$).

**Complexity**: $O(\sqrt{N} \log N)$ time, $O(1)$ space.

---

## Python 3

```python
import math

def all_same_digits(n, b):
    first = n % b
    while n:
        if n % b != first:
            return False
        n //= b
    return True

def min_base(N):
    if N < 3:
        return -1
    
    limit = math.isqrt(N)
    # Phase 1: bases producing >= 3 digits (b <= sqrt(N))
    for b in range(2, min(limit + 1, N - 1) + 1):
        if all_same_digits(N, b):
            return b

    # Phase 2: 2-digit representations "dd" with b > sqrt(N)
    for d in range(limit, 0, -1):
        if N % d == 0:
            b = N // d - 1
            if d < b and b >= 2:
                return b

    return N - 1

N = int(input().strip())
print(min_base(N))
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

bool all_same(ll n, ll b) {
    ll first = n % b;
    while (n) {
        if (n % b != first) return false;
        n /= b;
    }
    return true;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);

    ll N;
    if (!(cin >> N) || N < 3) {
        cout << -1 << "\n";
        return 0;
    }

    ll limit = (ll)sqrtl((long double)N);
    while (limit * limit > N) limit--;
    while ((limit + 1) * (limit + 1) <= N) limit++;

    // Phase 1: >= 3 digits (b <= sqrt(N))
    for (ll b = 2; b <= min(limit + 1, N - 1); b++) {
        if (all_same(N, b)) {
            cout << b << "\n";
            return 0;
        }
    }

    // Phase 2: 2 digits "dd" where N = d*(b+1)
    for (ll d = limit; d >= 1; d--) {
        if (N % d == 0) {
            ll b = N / d - 1;
            if (d < b && b >= 2) {
                cout << b << "\n";
                return 0;
            }
        }
    }

    cout << N - 1 << "\n";
    return 0;
}
```

---

## Edge Cases

| Input | Output | Explanation |
|---|---|---|
| `13` | `3` | `13` in base 3 = `111` |
| `12` | `5` | `12` in base 5 = `22` ($d=2, b=5$) |
| `231` | `20` | `231 = 11 * 21` = `BB` in base 20 |
| `7` | `2` | `7` in base 2 = `111` |
| `4` | `3` | `4` in base 3 = `11` |
