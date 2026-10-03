# Problem 19 — Largest Set with Product 1 mod N

**Tier**: Hard (Q3) | **Marks**: 50 | **Topic**: Number Theory / Euler's Totient & Wilson's Generalization

> [!CAUTION]
> **Online Trap**: Online solutions often compute $(N-1)!$ (which overflows 32-bit integers) or return $\varphi(N)$ unconditionally without checking group parity. Both lead to wrong answers on hidden test cases.

---

## Problem

Given a positive integer $N$, find the **size of the largest subset** of integers chosen from $[1, N-1]$ such that the **product of all elements in the subset** is congruent to $1 \pmod{N}$.

**Sample Input**:
```
9
```
**Sample Output**:
```
5
```
**Explanation**:
The integers in $[1, 8]$ coprime to 9 are $\{1, 2, 4, 5, 7, 8\}$ ($\varphi(9) = 6$).
Their total product is $1 \times 2 \times 4 \times 5 \times 7 \times 8 = 2240 \equiv 8 \equiv -1 \pmod{9}$.
By Gauss's generalization of Wilson's theorem, because 9 has a primitive root ($9 = 3^2$), the product of all coprime numbers is $\equiv -1 \pmod{9}$.
To obtain a product of $1 \pmod{9}$, we must drop the element $8 \equiv -1$.
The remaining subset $\{1, 2, 4, 5, 7\}$ has size **5** and product $280 \equiv 1 \pmod{9}$.

**Constraints**: $2 \leq N \leq 10^{12}$.

---

## Key Insight

> 1. Any element in the subset must be coprime to $N$ ($\gcd(x, N) = 1$), because if $\gcd(x, N) > 1$, no multiple can ever be congruent to $1 \pmod N$. Thus, all chosen elements must come from the group of units $U_N = \{x \in [1, N-1] \mid \gcd(x, N) = 1\}$, which has size $\varphi(N)$.
> 2. By **Gauss's Generalization of Wilson's Theorem**, the product $P = \prod_{x \in U_N} x \pmod N$ is:
>    $$P \equiv \begin{cases} -1 \pmod N & \text{if } N \in \{2, 4, p^k, 2p^k\} \text{ for any odd prime } p \\ +1 \pmod N & \text{otherwise} \end{cases}$$
> 3. If $P \equiv 1 \pmod N$, we can take the entire set $U_N$, giving size $\varphi(N)$.
> 4. If $P \equiv -1 \pmod N$ (and $N > 2$):
>    Since $-1 \not\equiv 1 \pmod N$, the full set cannot be used. We can drop the single element $N-1 \equiv -1 \in U_N$, leaving $\varphi(N) - 1$ elements whose product is $(-1) / (-1) \equiv 1 \pmod N$.
>    Hence, the maximum subset size is $\varphi(N) - 1$.

---

## Approach

1. Compute Euler's Totient $\varphi(N)$ in $O(\sqrt{N})$.
2. Determine if $N$ has a primitive root (i.e., $N \in \{1, 2, 4\}$ or $N = p^k$ or $N = 2p^k$ for an odd prime $p$).
3. If $N > 2$ and $N$ has a primitive root, return $\varphi(N) - 1$.
4. Otherwise, return $\varphi(N)$.

**Complexity**: $O(\sqrt{N})$ time, $O(1)$ space.

---

## Python 3

```python
def euler_totient(n):
    result, temp, p = n, n, 2
    while p * p <= temp:
        if temp % p == 0:
            while temp % p == 0:
                temp //= p
            result -= result // p
        p += 1
    if temp > 1:
        result -= result // temp
    return result

def has_primitive_root(n):
    """Returns True iff n is 1, 2, 4, p^k, or 2*p^k for an odd prime p."""
    if n in (1, 2, 4):
        return True
    if n % 2 == 0:
        n //= 2
    if n % 2 == 0:
        return False
    # n must be p^k for an odd prime p
    p = 3
    while p * p <= n:
        if n % p == 0:
            break
        p += 2
    else:
        p = n
    while n % p == 0:
        n //= p
    return n == 1

def largest_set_product_one(N):
    phi = euler_totient(N)
    if N > 2 and has_primitive_root(N):
        return phi - 1
    return phi

N = int(input().strip())
print(largest_set_product_one(N))
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

bool has_primitive_root(ll n) {
    if (n == 1 || n == 2 || n == 4) return true;
    if (n % 2 == 0) n /= 2;
    if (n % 2 == 0) return false;
    ll p = n;
    for (ll d = 3; d * d <= n; d += 2) {
        if (n % d == 0) {
            p = d;
            break;
        }
    }
    while (n % p == 0) n /= p;
    return n == 1;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);

    ll N;
    if (!(cin >> N)) return 0;

    ll phi = euler_totient(N);
    if (N > 2 && has_primitive_root(N)) {
        cout << phi - 1 << "\n";
    } else {
        cout << phi << "\n";
    }
    return 0;
}
```

---

## Edge Cases

| N | φ(N) | Primitive Root? | Max Subset Size | Notes |
|---|---|---|---|---|
| `3` | 2 | Yes ($3^1$) | **1** | Subset `{1}` |
| `8` | 4 | No ($2^3$) | **4** | $\{1, 3, 5, 7\}$ has product $105 \equiv 1 \pmod 8$ |
| `9` | 6 | Yes ($3^2$) | **5** | Drop 8; product is $1 \pmod 9$ |
| `12` | 4 | No ($2^2 \times 3$) | **4** | $\{1, 5, 7, 11\}$ has product $385 \equiv 1 \pmod{12}$ |
| `10` | 4 | Yes ($2 \times 5$) | **3** | Drop 9; product is $1 \pmod{10}$ |
