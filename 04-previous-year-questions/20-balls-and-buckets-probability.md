# Problem 20 — Balls and Buckets: Colour Probability

**Tier**: Hard (Q3) | **Marks**: 50 | **Topic**: Probability / Dynamic Programming (Poisson-Binomial Distribution)

---

## Problem

You have $B$ buckets. Each bucket $i$ contains $r_i$ red balls and $g_i$ green balls. You randomly draw **one ball from each bucket** (uniformly at random). Find the **probability** that the total number of red balls drawn across all buckets is **exactly $K$**.

Output the answer as a floating-point value rounded to 6 decimal places.

**Sample Input**:
```
3 2
2 3
1 4
3 2
```
**Sample Output**:
```
0.296000
```
**Explanation**:
For each bucket:
- Bucket 1: $P(R_1) = 2/(2+3) = 2/5 = 0.4$, $P(G_1) = 3/5 = 0.6$
- Bucket 2: $P(R_2) = 1/(1+4) = 1/5 = 0.2$, $P(G_2) = 4/5 = 0.8$
- Bucket 3: $P(R_3) = 3/(3+2) = 3/5 = 0.6$, $P(G_3) = 2/5 = 0.4$

To draw exactly 2 red balls, we can draw:
1. Red from 1 & 2, Green from 3: $0.4 \times 0.2 \times 0.4 = 0.032$
2. Red from 1 & 3, Green from 2: $0.4 \times 0.8 \times 0.6 = 0.192$
3. Red from 2 & 3, Green from 1: $0.6 \times 0.2 \times 0.6 = 0.072$

Total probability $= 0.032 + 0.192 + 0.072 = 0.296000$.

**Constraints**: $1 \leq B \leq 100$, $1 \leq r_i + g_i \leq 100$, $0 \leq K \leq B$.

---

## Key Insight

> **Convolution DP**:
> Let `dp[j]` be the probability of having drawn exactly $j$ red balls from the first $i$ buckets.
> When processing bucket $i$ with $P(R) = p$:
> $$\text{new\_dp}[j] = \text{dp}[j] \times (1 - p) + \text{dp}[j-1] \times p$$
> This computes the convolution of $B$ independent Bernoulli random variables in $O(B^2)$ time.

---

## Approach

1. Initialize `dp = [0.0] * (B + 1)`, `dp[0] = 1.0`.
2. For each bucket $(r_i, g_i)$:
   - $p = r_i / (r_i + g_i)$
   - Update `dp` backwards from $B$ down to 0:
     - `dp[j] = dp[j] * (1 - p) + (dp[j-1] * p if j > 0 else 0)`
3. Return `dp[K]` formatted to 6 decimal places.

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
        p_red = r / total
        p_green = g / total
        new_dp = [0.0] * (B + 1)
        for j in range(B + 1):
            if dp[j] == 0:
                continue
            new_dp[j] += dp[j] * p_green
            if j + 1 <= B:
                new_dp[j + 1] += dp[j] * p_red
        dp = new_dp

    return dp[K]

import sys
lines = sys.stdin.read().split()
if lines:
    B, K = int(lines[0]), int(lines[1])
    buckets = []
    idx = 2
    for _ in range(B):
        buckets.append((int(lines[idx]), int(lines[idx + 1])))
        idx += 2
    print(f"{ball_probability(buckets, K):.6f}")
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);

    int B, K;
    if (!(cin >> B >> K)) return 0;

    vector<pair<int,int>> buckets(B);
    for (int i = 0; i < B; i++) {
        cin >> buckets[i].first >> buckets[i].second;
    }

    vector<double> dp(B + 1, 0.0);
    dp[0] = 1.0;

    for (int i = 0; i < B; i++) {
        double r = buckets[i].first;
        double g = buckets[i].second;
        double total = r + g;
        double p_red = r / total;
        double p_green = g / total;

        vector<double> ndp(B + 1, 0.0);
        for (int j = 0; j <= B; j++) {
            if (dp[j] == 0.0) continue;
            ndp[j] += dp[j] * p_green;
            if (j + 1 <= B) {
                ndp[j + 1] += dp[j] * p_red;
            }
        }
        dp = ndp;
    }

    cout << fixed << setprecision(6) << dp[K] << "\n";
    return 0;
}
```

---

## Edge Cases

| Scenario | Input | Output | Reason |
|---|---|---|---|
| K = 0 | 2 buckets: (1, 1), (1, 1) | `0.250000` | Only green drawn: $(1/2) \times (1/2) = 0.25$ |
| K = B | 2 buckets: (1, 1), (1, 1) | `0.250000` | Only red drawn: $(1/2) \times (1/2) = 0.25$ |
| Single bucket | 1 bucket: (1, 1), K = 1 | `0.500000` | $1/2 = 0.5$ |
