# Problem 2 — Next Greater Element

**Tier**: Easy (Q1) | **Marks**: 20 | **Topic**: Stack / Monotonic

---

## Problem

Given an array of integers, for each element find the **next greater element** to its right. If no greater element exists, output `-1`.

**Sample Input**:
```
arr = [4, 5, 2, 10, 8]
```
**Sample Output**:
```
[5, 10, 10, -1, -1]
```

**Constraints**: $1 \leq N \leq 10^5$, $0 \leq arr[i] \leq 10^9$.

---

## Key Insight

> Use a **monotonic decreasing stack**. Traverse right-to-left, maintaining a stack of candidates. For each element, pop elements from the stack that are ≤ current — they can never be the "next greater" for any element to the left.

---

## Approach

1. Initialize `result = [-1] * N` and an empty stack.
2. Traverse from right (`i = N-1`) to left (`i = 0`):
   - Pop from stack while stack top ≤ `arr[i]`.
   - If stack is non-empty, `result[i] = stack top`.
   - Push `arr[i]` onto stack.
3. Return `result`.

**Complexity**: $O(N)$ time, $O(N)$ space — each element pushed/popped at most once.

---

## Python 3

```python
def next_greater(arr):
    n = len(arr)
    result = [-1] * n
    stack = []  # stores values
    for i in range(n - 1, -1, -1):
        while stack and stack[-1] <= arr[i]:
            stack.pop()
        if stack:
            result[i] = stack[-1]
        stack.append(arr[i])
    return result

# --- Driver ---
arr = list(map(int, input().split()))
print(*next_greater(arr))
```

## C++ 17

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);

    int n; cin >> n;
    vector<int> arr(n);
    for (int& x : arr) cin >> x;

    vector<int> result(n, -1);
    stack<int> st;  // stores values

    for (int i = n - 1; i >= 0; i--) {
        while (!st.empty() && st.top() <= arr[i]) st.pop();
        if (!st.empty()) result[i] = st.top();
        st.push(arr[i]);
    }

    for (int i = 0; i < n; i++)
        cout << result[i] << " \n"[i == n-1];
    return 0;
}
```

---

## Edge Cases

| Input | Output | Reason |
|---|---|---|
| `[5, 4, 3, 2, 1]` | `[-1, -1, -1, -1, -1]` | Strictly decreasing — no NGE |
| `[1, 2, 3, 4, 5]` | `[2, 3, 4, 5, -1]` | Strictly increasing — NGE is adjacent |
| `[3]` | `[-1]` | Single element |
