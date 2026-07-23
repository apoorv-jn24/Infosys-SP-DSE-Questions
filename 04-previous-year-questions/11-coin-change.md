# Problem 11 — Coin Change

**Tier**: Medium (Q2) | **Marks**: 30 | **Topic**: Dynamic Programming (Unbounded Knapsack)

---

## Problem

Given an array of coin denominations and a target amount $S$, find the **minimum number of coins** needed to make exactly $S$. If it's not possible, return `-1`.

**Sample Input**:
```
coins = [1, 5, 6, 9]
S = 11
```
**Sample Output**:
```
2
```
**Explanation**: `9 + 1 + 1 = 11` uses 3 coins, but `6 + 5 = 11` uses **2 coins**.

**Constraints**: $1 \leq |coins| \leq 12$, $1 \leq S \leq 10^4$, $1 \leq coins[i] \leq S$.

---

## Key Insight

> **Unbounded Knapsack DP**: `dp[w]` = minimum coins to make amount `w`. Each coin can be reused unlimited times. Unlike 0/1 knapsack, iterate the weight dimension forward (not backward).

---

## Approach

1. `dp = [INF] * (S+1)`, `dp[0] = 0`.
2. For each amount `w` from `1` to `S`:
   - For each coin `c`: if `c <= w` and `dp[w-c] + 1 < dp[w]`: update.
3. Return `dp[S]` if `< INF`, else `-1`.

**Complexity**: $O(S \times |coins|)$ time, $O(S)$ space.

---

## Python 3

```python
def coin_change(coins, S):
    INF = float('inf')
    dp = [INF] * (S + 1)
    dp[0] = 0
    for w in range(1, S + 1):
        for c in coins:
            if c <= w and dp[w - c] + 1 < dp[w]:
                dp[w] = dp[w - c] + 1
    return dp[S] if dp[S] < INF else -1

coins = list(map(int, input().split()))
S = int(input())
print(coin_change(coins, S))
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false); cin.tie(NULL);
    int n, S; cin >> n >> S;
    vector<int> coins(n);
    for (int& x : coins) cin >> x;

    const int INF = 1e9;
    vector<int> dp(S + 1, INF);
    dp[0] = 0;
    for (int w = 1; w <= S; w++)
        for (int c : coins)
            if (c <= w && dp[w-c] < INF)
                dp[w] = min(dp[w], dp[w-c] + 1);

    cout << (dp[S] == INF ? -1 : dp[S]) << "\n";
    return 0;
}
```

---

## Edge Cases

| coins | S | Output |
|---|---|---|
| `[2]` | `3` | `-1` |
| `[1]` | `0` | `0` |
| `[1, 2, 5]` | `11` | `3` (5+5+1) |
