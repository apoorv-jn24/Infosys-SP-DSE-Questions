# Problem 14 — Counting Divisible Arrays

**Tier**: Hard (Q3) | **Marks**: 50 | **Topic**: Number Theory / Chinese Remainder Theorem / Generating Functions

---

## Problem

Given integers $N$ and $K$, count the number of arrays of length $K$ with elements chosen from $[1, N]$ such that the **product of all elements is divisible by $N$**. Output the answer modulo $10^9 + 7$.

**Sample Input**:
```
4 2
```
**Sample Output**:
```
8
```
**Explanation**: All 8 valid pairs $(a, b) \in [1, 4]^2$ with $(a \cdot b) \bmod 4 = 0$ are:
$(1,4), (2,2), (2,4), (3,4), (4,1), (4,2), (4,3), (4,4)$.

**Constraints**: $1 \leq N \leq 10^6$, $1 \leq K \leq 10^5$.

---

## Key Insight

> 1. Factorize $N = \prod_{i=1}^m p_i^{a_i}$ into distinct prime powers.
> 2. By the Chinese Remainder Theorem (CRT), choosing an integer in $[1, N]$ uniformly at random is equivalent to choosing independent residues modulo each $p_i^{a_i}$. Therefore, the problem factors independently across each prime power $p^a$:
>    $$\text{Answer} = \prod_{p^a \parallel N} \text{ValidCount}(p, a, K) \pmod{10^9 + 7}$$
> 3. For a single prime power $p^a$, the product of elements is divisible by $p^a$ if and only if the sum of $p$-adic valuations satisfies $\sum_{j=1}^K v_p(arr[j]) \geq a$.
> 4. In $[1, p^a]$, the number of residues with $v_p(x) = v$ (for $0 \leq v < a$) is:
>    $$c[v] = p^{a - v} - p^{a - v - 1}$$
> 5. The generating function for the sum of valuations is $P(x) = \sum_{v=0}^{a-1} c[v] x^v$. Computing $P(x)^K \bmod x^a$ via polynomial binary exponentiation gives the number of tuples whose valuation sum is $< a$ (the "bad" tuples).
> 6. $\text{ValidCount}(p, a, K) = (p^a)^K - \sum_{v=0}^{a-1} [x^v](P(x)^K \bmod x^a)$.

---

## Approach

1. Factorize $N$ into prime powers $p^a$.
2. For each $p^a$:
   - Build polynomial $c$ of degree $a$ where $c[v] = p^{a-v} - p^{a-v-1}$.
   - Compute $res = c^K \bmod x^a$ using polynomial multiplication in $O(a^2 \log K)$.
   - $\text{bad} = \sum_{v=0}^{a-1} res[v]$.
   - $\text{valid} = ((p^a)^K - \text{bad}) \pmod{10^9 + 7}$.
3. Multiply the valid counts across all prime factors modulo $10^9 + 7$.

**Complexity**: $O(\sqrt{N} + \omega(N) \cdot a^2 \log K)$ time where $a \leq 20$, $O(a)$ space.

---

## Python 3

```python
MOD = 10**9 + 7

def factorize(n):
    factors = {}
    d = 2
    while d * d <= n:
        while n % d == 0:
            factors[d] = factors.get(d, 0) + 1
            n //= d
        d += 1
    if n > 1:
        factors[n] = factors.get(n, 0) + 1
    return factors

def poly_mul(A, B, deg):
    C = [0] * deg
    for i, a in enumerate(A):
        if a:
            for j in range(deg - i):
                C[i + j] = (C[i + j] + a * B[j]) % MOD
    return C

def poly_pow(P, k, deg):
    result = [1] + [0] * (deg - 1)
    while k:
        if k & 1:
            result = poly_mul(result, P, deg)
        P = poly_mul(P, P, deg)
        k >>= 1
    return result

def count_divisible_arrays(N, K):
    ans = 1
    for p, a in factorize(N).items():
        # c[v] = residues mod p^a with p-adic valuation exactly v
        c = [(pow(p, a - v, MOD) - pow(p, a - v - 1, MOD) + MOD) % MOD for v in range(a)]
        bad = sum(poly_pow(c, K, a)) % MOD
        total = pow(p, a * K, MOD)
        ans = (ans * (total - bad + MOD)) % MOD
    return ans

N, K = map(int, input().split())
print(count_divisible_arrays(N, K))
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const ll MOD = 1e9 + 7;

ll power(ll b, ll e) {
    ll r = 1; b %= MOD;
    while (e > 0) {
        if (e & 1) r = (r * b) % MOD;
        b = (b * b) % MOD;
        e >>= 1;
    }
    return r;
}

vector<ll> polyMul(const vector<ll>& A, const vector<ll>& B, int deg) {
    vector<ll> C(deg, 0);
    for (int i = 0; i < deg; i++) {
        if (!A[i]) continue;
        for (int j = 0; i + j < deg; j++) {
            C[i + j] = (C[i + j] + A[i] * B[j]) % MOD;
        }
    }
    return C;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);

    ll N, K;
    if (!(cin >> N >> K)) return 0;

    ll ans = 1, temp = N;
    for (ll p = 2; p * p <= temp || temp > 1; p++) {
        if (p * p > temp) p = temp;
        if (temp % p != 0) continue;

        int a = 0;
        while (temp % p == 0) {
            temp /= p;
            a++;
        }

        vector<ll> pw(a + 1, 1);
        for (int i = 1; i <= a; i++) pw[i] = pw[i - 1] * p;

        vector<ll> c(a), res(a, 0);
        res[0] = 1;
        for (int v = 0; v < a; v++) {
            c[v] = (pw[a - v] - pw[a - v - 1]) % MOD;
        }

        for (ll e = K; e > 0; e >>= 1) {
            if (e & 1) res = polyMul(res, c, a);
            c = polyMul(c, c, a);
        }

        ll bad = 0;
        for (ll x : res) bad = (bad + x) % MOD;
        ll total = power(p, (ll)a * K);
        ans = (ans * ((total - bad + MOD) % MOD)) % MOD;
    }

    cout << ans << "\n";
    return 0;
}
```

---

## Edge Cases

| N | K | Output | Explanation |
|---|---|---|---|
| 4 | 2 | 8 | Pairs from $[1, 4]$ divisible by 4 |
| 1 | 5 | 1 | $1^5 = 1$, always divisible by 1 |
| 7 | 3 | 127 | Prime $N=7$: $7^3 - 6^3 = 343 - 216 = 127$ |
