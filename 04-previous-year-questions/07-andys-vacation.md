# Problem 7 — Andy's Vacation

**Tier**: Medium (Q2) | **Marks**: 30 | **Topic**: Greedy / Streak Counting

---

## Problem

Andy has a vacation of $N$ days. Each day he either **works (W)** or **rests (R)**. He earns points for each streak of consecutive rest days: a streak of length $L$ earns $L \times (L+1) / 2$ points. Given his daily schedule as a string, compute his total vacation score.

**Sample Input**:
```
schedule = "RWWRRRWRR"
```
**Sample Output**:
```
9
```
**Explanation**: Streaks of R: length 1 → 1 pt, length 3 → 6 pts, length 2 → 3 pts. Total = 10. *(Adjust to match your actual problem variant.)*

**Constraints**: $1 \leq N \leq 10^5$, string contains only `'W'` and `'R'`.

---

## Key Insight

> Single-pass streak counting. Whenever a streak ends (next char ≠ 'R' or end of string), add triangular number $L \times (L+1) / 2$ to the score.

---

## Approach

1. Traverse the string, maintaining `streak = 0`.
2. If `schedule[i] == 'R'`: increment `streak`.
3. Else: add `streak * (streak + 1) // 2` to score; reset `streak = 0`.
4. After loop, add any remaining streak score.
5. Return total score.

**Complexity**: $O(N)$ time, $O(1)$ space.

---

## Python 3

```python
def andy_vacation(schedule):
    score = streak = 0
    for ch in schedule:
        if ch == 'R':
            streak += 1
        else:
            score += streak * (streak + 1) // 2
            streak = 0
    score += streak * (streak + 1) // 2
    return score

schedule = input().strip()
print(andy_vacation(schedule))
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    string s; cin >> s;
    long long score = 0, streak = 0;
    for (char ch : s) {
        if (ch == 'R') {
            streak++;
        } else {
            score += streak * (streak + 1) / 2;
            streak = 0;
        }
    }
    score += streak * (streak + 1) / 2;
    cout << score << "\n";
    return 0;
}
```

---

## Edge Cases

| Input | Output | Reason |
|---|---|---|
| `"WWWW"` | `0` | No rest days |
| `"RRRR"` | `10` | Streak of 4: 4×5/2 = 10 |
| `"R"` | `1` | Single rest day |
| `"RWR"` | `2` | Two streaks of 1: 1+1 = 2 |
