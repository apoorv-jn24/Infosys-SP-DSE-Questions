# Problem 6 — Monster Quest

**Tier**: Medium (Q2) | **Marks**: 30 | **Topic**: Greedy / Sorting

---

## Problem

You have $N$ heroes, each with attack power $a_i$, and $M$ monsters each with health $h_j$. A hero can defeat a monster if $a_i \geq h_j$. Each hero can fight **at most one monster** per round. Find the **maximum number of monsters** that can be defeated in a single round.

**Sample Input**:
```
heroes  = [5, 1, 3, 7, 2]
monsters = [3, 6, 2, 8, 1]
```
**Sample Output**:
```
4
```
**Explanation**: Sorted heroes `[1, 2, 3, 5, 7]` and monsters `[1, 2, 3, 6, 8]`: Hero 1 beats monster 1; hero 2 beats monster 2; hero 3 beats monster 3; hero 7 beats monster 6 → 4 defeats.

**Constraints**: $1 \leq N, M \leq 10^5$, $1 \leq a_i, h_j \leq 10^9$.

---

## Key Insight

> **Greedy exchange argument**: Sort both arrays. Match the weakest available hero to the weakest available monster they can defeat. Never "waste" a strong hero on a weak monster when they're needed for a stronger one.

---

## Approach

1. Sort `heroes` and `monsters` ascending.
2. Use two pointers `i` (heroes) and `j` (monsters), count = 0.
3. If `heroes[i] >= monsters[j]`: match made, increment both `i`, `j`, and count.
4. Else: hero is too weak — advance `i` only.
5. Return count.

**Complexity**: $O(N \log N + M \log M)$ time, $O(1)$ extra space.

---

## Python 3

```python
def monster_quest(heroes, monsters):
    heroes.sort(); monsters.sort()
    i = j = count = 0
    while i < len(heroes) and j < len(monsters):
        if heroes[i] >= monsters[j]:
            count += 1; j += 1
        i += 1
    return count

heroes  = list(map(int, input().split()))
monsters = list(map(int, input().split()))
print(monster_quest(heroes, monsters))
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false); cin.tie(NULL);
    int n, m; cin >> n >> m;
    vector<int> a(n), h(m);
    for (int& x : a) cin >> x;
    for (int& x : h) cin >> x;
    sort(a.begin(), a.end());
    sort(h.begin(), h.end());

    int i = 0, j = 0, count = 0;
    while (i < n && j < m) {
        if (a[i] >= h[j]) { count++; j++; }
        i++;
    }
    cout << count << "\n";
    return 0;
}
```

---

## Edge Cases

| Scenario | Output |
|---|---|
| All heroes weaker than all monsters | 0 |
| All heroes stronger than all monsters | min(N, M) |
| N = 1, M = 1, hero weaker | 0 |
