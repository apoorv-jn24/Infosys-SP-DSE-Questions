# Problem 16 — Longest Increasing Path in Matrix

**Tier**: Hard (Q3) | **Marks**: 50 | **Topic**: DFS + Memoization

---

## Problem

Given an $N \times M$ matrix of integers, find the length of the **longest strictly increasing path**. From each cell you can move in 4 directions (up, down, left, right). You cannot move diagonally or wrap around.

**Sample Input**:
```
matrix = [
  [9, 9, 4],
  [6, 6, 8],
  [2, 1, 1]
]
```
**Sample Output**:
```
4
```
**Explanation**: Path `1 → 2 → 6 → 9` has length 4.

**Constraints**: $1 \leq N, M \leq 200$, $0 \leq matrix[i][j] \leq 2^{31} - 1$.

---

## Key Insight

> DFS with **memoization** (top-down DP on DAG). Since we only move to strictly larger values, the grid forms a DAG — no cycles. `memo[i][j]` = longest increasing path starting from cell `(i, j)`.

> [!WARNING]
> Do NOT use recursive DFS without memoization — it leads to $O(4^{N \times M})$ exponential time. With memoization, each cell is computed exactly once: $O(N \times M)$.

---

## Approach

1. `memo = [[-1]*M for _ in range(N)]`.
2. DFS from each cell:
   - If `memo[i][j] != -1`: return cached value.
   - Try all 4 neighbors; if neighbor value > current, recurse.
   - `memo[i][j] = 1 + max(valid_neighbor_paths)`.
3. Return `max(memo)`.

**Complexity**: $O(N \times M)$ time, $O(N \times M)$ space.

---

## Python 3

```python
import sys
sys.setrecursionlimit(10**5)

def longest_increasing_path(matrix):
    if not matrix: return 0
    n, m = len(matrix), len(matrix[0])
    memo = [[-1]*m for _ in range(n)]
    dirs = [(-1,0),(1,0),(0,-1),(0,1)]

    def dfs(r, c):
        if memo[r][c] != -1:
            return memo[r][c]
        best = 1
        for dr, dc in dirs:
            nr, nc = r+dr, c+dc
            if 0<=nr<n and 0<=nc<m and matrix[nr][nc] > matrix[r][c]:
                best = max(best, 1 + dfs(nr, nc))
        memo[r][c] = best
        return best

    return max(dfs(i, j) for i in range(n) for j in range(m))

n, m = map(int, input().split())
matrix = [list(map(int, input().split())) for _ in range(n)]
print(longest_increasing_path(matrix))
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;

int n, m;
vector<vector<int>> mat, memo;
int dirs[4][2] = {{-1,0},{1,0},{0,-1},{0,1}};

int dfs(int r, int c) {
    if (memo[r][c] != -1) return memo[r][c];
    int best = 1;
    for (auto& d : dirs) {
        int nr = r+d[0], nc = c+d[1];
        if (nr>=0&&nr<n&&nc>=0&&nc<m && mat[nr][nc]>mat[r][c])
            best = max(best, 1+dfs(nr,nc));
    }
    return memo[r][c] = best;
}

int main() {
    ios::sync_with_stdio(false); cin.tie(NULL);
    cin >> n >> m;
    mat.assign(n, vector<int>(m));
    memo.assign(n, vector<int>(m, -1));
    for (auto& row : mat) for (int& x : row) cin >> x;

    int ans = 0;
    for (int i=0;i<n;i++) for (int j=0;j<m;j++) ans = max(ans, dfs(i,j));
    cout << ans << "\n";
    return 0;
}
```

---

## Edge Cases

| Matrix | Output |
|---|---|
| `[[1]]` | `1` |
| `[[3,4,5],[3,2,6],[2,2,1]]` | `4` (1→2→3→4) |
