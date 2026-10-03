# Problem 10 — Number of Islands

**Tier**: Medium (Q2) | **Marks**: 30 | **Topic**: Graphs / BFS / DFS on Grid

---

## Problem

Given an $N \times M$ grid of `'1'` (land) and `'0'` (water), count the **number of islands**. An island is a maximal group of adjacent land cells connected horizontally or vertically.

**Sample Input**:
```
grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
```
**Sample Output**:
```
3
```

**Constraints**: $1 \leq N, M \leq 300$.

---

## Key Insight

> BFS/DFS flood-fill. For each unvisited land cell (`'1'`), increment island count and flood-fill all reachable land cells, marking them visited (change to `'0'`).

> [!WARNING]
> For large grids ($300 \times 300 = 90000$ cells), recursive DFS can hit Python's recursion limit. Use **iterative BFS** with a queue.

---

## Approach (BFS)

1. Count = 0.
2. For each cell `(i, j)`:
   - If `grid[i][j] == '1'`: Count++, BFS from `(i, j)`.
   - BFS: push `(i, j)` into queue, mark as `'0'`. Pop cells, push all `'1'` neighbors, marking each `'0'`.
3. Return Count.

**Complexity**: $O(N \times M)$ time, $O(N \times M)$ space (queue).

---

## Python 3

```python
from collections import deque

def num_islands(grid):
    if not grid: return 0
    n, m = len(grid), len(grid[0])
    count = 0

    for i in range(n):
        for j in range(m):
            if grid[i][j] == '1':
                count += 1
                q = deque([(i, j)])
                grid[i][j] = '0'
                while q:
                    r, c = q.popleft()
                    for dr, dc in [(-1,0),(1,0),(0,-1),(0,1)]:
                        nr, nc = r+dr, c+dc
                        if 0 <= nr < n and 0 <= nc < m and grid[nr][nc] == '1':
                            grid[nr][nc] = '0'
                            q.append((nr, nc))
    return count

n, m = map(int, input().split())
grid = [input().split() for _ in range(n)]
print(num_islands(grid))
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false); cin.tie(NULL);
    int n, m; cin >> n >> m;
    vector<string> g(n);
    for (auto& row : g) cin >> row;

    int count = 0;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (g[i][j] == '1') {
                count++;
                queue<pair<int,int>> q;
                q.push({i, j}); g[i][j] = '0';
                while (!q.empty()) {
                    pair<int,int> cur = q.front(); q.pop();
                    int r = cur.first, c = cur.second;
                    int dr[] = {-1, 1, 0, 0};
                    int dc[] = {0, 0, -1, 1};
                    for (int d = 0; d < 4; d++) {
                        int nr = r + dr[d], nc = c + dc[d];
                        if (nr >= 0 && nr < n && nc >= 0 && nc < m && g[nr][nc] == '1') {
                            g[nr][nc] = '0';
                            q.push({nr, nc});
                        }
                    }
                }
            }
        }
    }
    cout << count << "\n";
    return 0;
}
```

---

## Edge Cases

| Scenario | Output |
|---|---|
| All water | `0` |
| All land | `1` |
| Single cell `'1'` | `1` |
