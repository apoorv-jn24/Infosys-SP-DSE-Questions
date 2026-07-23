# Problem 20 — Balls and Buckets: Colour Probability

**Tier**: Hard (Q3) | **Marks**: 50 | **Topic**: Probability / Combinatorics

---

## Problem

You have $B$ buckets. Each bucket $i$ contains $r_i$ red balls and $g_i$ green balls. You randomly draw **one ball from each bucket** (uniformly at random). Find the **probability** that the total number of red balls drawn is **exactly $K$**.

Output the answer as a fraction in lowest terms (or as a floating-point value to 6 decimal places, per problem statement).

**Sample Input**:
```
buckets = [(2, 3), (1, 4), (3, 2)]   # (red, green) per bucket
K = 2
```
**Sample Output**:
```
0.342857
```

**Constraints**: $1 \leq B \leq 20$, $1 \leq r_i + g_i \leq 100$, $0 \leq K \leq B$.

---

## Key Insight

> **DP over buckets and count of red balls drawn**. `dp[j]` = probability of drawing exactly $j$ red balls from the first $i$ buckets. For each bucket $i$, update DP by considering drawing red or green.

This is equivalent to computing a convolution of Bernoulli random variables.

---

## Approach

1. `dp = [0.0] * (B+1)`, `dp[0] = 1.0`.
2. For each bucket $(r_i, g_i)$:
   - `total = r_i + g_i`.
   - `p_red = r_i / total`, `p_green = g_i / total`.
   - Update DP right-to-left (new array to avoid in-place conflicts):
     - `new_dp[j] = dp[j-1] * p_red + dp[j] * p_green`.
3. Return `dp[K]`.

**Complexity**: $O(B^2)$ time, $O(B)$ space.

---

## Python 3

```python
def ball_probability(buckets, K):
    B = len(buckets)
    dp = [0.0] * (B + 1)
    dp[0] = 1.0

    for r, g in buckets:
        total = r + g
        p_red   = r / total
        p_green = g / total
        new_dp = [0.0] * (B + 1)
        for j in range(B + 1):
            if dp[j] == 0: continue
            # Draw green from this bucket
            new_dp[j]   += dp[j] * p_green
            # Draw red from this bucket
            if j + 1 <= B:
                new_dp[j+1] += dp[j] * p_red
        dp = new_dp

    return dp[K]

B = int(input())
buckets = [tuple(map(int, input().split())) for _ in range(B)]
K = int(input())
print(f"{ball_probability(buckets, K):.6f}")
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false); cin.tie(NULL);
    int B, K; cin >> B >> K;
    vector<pair<int,int>> buckets(B);
    for (auto& [r,g] : buckets) cin >> r >> g;

    vector<double> dp(B + 1, 0.0);
    dp[0] = 1.0;

    for (auto [r, g] : buckets) {
        double total = r + g;
        double p_red = r / total, p_green = g / total;
        vector<double> ndp(B + 1, 0.0);
        for (int j = 0; j <= B; j++) {
            if (dp[j] == 0) continue;
            ndp[j] += dp[j] * p_green;
            if (j + 1 <= B) ndp[j+1] += dp[j] * p_red;
        }
        dp = ndp;
    }
    cout << fixed << setprecision(6) << dp[K] << "\n";
    return 0;
}
```

---

## Edge Cases

| Scenario | Output |
|---|---|
| K = 0 (draw only green) | Product of all $g_i / (r_i + g_i)$ |
| K = B (draw all red) | Product of all $r_i / (r_i + g_i)$ |
| Single bucket (1R, 1G), K=1 | `0.500000` |
