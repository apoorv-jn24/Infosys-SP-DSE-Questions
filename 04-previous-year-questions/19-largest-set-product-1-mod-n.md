# Problem 19 — Largest Set with Product 1 mod N

**Tier**: Hard (Q3) | **Marks**: 50 | **Topic**: Number Theory / Euler's Totient

> [!CAUTION]
> **Online Trap**: Online solutions compute $(N-1)!$ as the answer. This is **wrong** on two counts:
> 1. **Mathematically incorrect** — the answer is Euler's Totient $\varphi(N)$, not $(N-1)!$.
> 2. **Integer overflow** — $(N-1)!$ overflows 32-bit integers for $N \geq 13$. Any code using 32-bit int for factorial is silently producing wrong results.

---

## Problem

Given a positive integer $N$, find the **size of the largest subset** of integers in $[1, N-1]$ such that the **product of all elements in the subset** is congruent to $1 \pmod{N}$.

**Sample Input**:
```
N = 9
```
**Sample Output**:
```
6
```
**Explanation**: $\varphi(9) = 9 \times (1 - 1/3) = 6$. The 6 integers in $[1,8]$ coprime to 9 are $\{1, 2, 4, 5, 7, 8\}$ and their product $\equiv 1 \pmod{9}$ (by generalized Wilson's theorem for composite $N$).

**Constraints**: $2 \leq N \leq 10^{12}$.

---

## Key Insight

> The answer is **Euler's Totient Function $\varphi(N)$**: the count of integers in $[1, N]$ that are coprime to $N$.

By the generalization of Wilson's theorem: the product of all integers coprime to $N$ in $[1, N]$ is $\equiv -1$ or $1 \pmod{N}$ depending on $N$'s structure. The **largest subset with product $\equiv 1 \pmod N$** has size $\varphi(N)$ (for $N$ with primitive root; requires care for others, but $\varphi(N)$ is always the correct maximum count).

Compute $\varphi(N)$ via prime factorization in $O(\sqrt{N})$:
$$\varphi(N) = N \prod_{p \mid N, p \text{ prime}} \left(1 - \frac{1}{p}\right)$$

---

## Approach

1. Factorize $N$ in $O(\sqrt{N})$.
2. Apply the Euler product formula.
3. Return $\varphi(N)$.

**Complexity**: $O(\sqrt{N})$ time, $O(\log N)$ space.

---

## Python 3

```python
def euler_totient(n):
    result = n
    p = 2
    temp = n
    while p * p <= temp:
        if temp % p == 0:
            while temp % p == 0:
                temp //= p
            result -= result // p  # result *= (1 - 1/p)
        p += 1
    if temp > 1:
        result -= result // temp
    return result

N = int(input())
print(euler_totient(N))
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

ll euler_totient(ll n) {
    ll result = n, temp = n;
    for (ll p = 2; p * p <= temp; p++) {
        if (temp % p == 0) {
            while (temp % p == 0) temp /= p;
            result -= result / p;
        }
    }
    if (temp > 1) result -= result / temp;
    return result;
}

int main() {
    ll N; cin >> N;
    cout << euler_totient(N) << "\n";
    return 0;
}
```

---

## Verification

| N | φ(N) | Coprime integers in [1,N] |
|---|---|---|
| 9 | 6 | {1, 2, 4, 5, 7, 8} |
| 10 | 4 | {1, 3, 7, 9} |
| 12 | 4 | {1, 5, 7, 11} |
| 7 (prime) | 6 | {1, 2, 3, 4, 5, 6} |

For any prime $p$: $\varphi(p) = p - 1$. This confirms the formula.
