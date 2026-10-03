# Contributing Guidelines

Thank you for helping keep this preparation guide rigorous, accurate, and up-to-date!

Mathematical and algorithmic corrections are the most valuable contributions to this repository.

---

## Reporting a Problem or Bug

If you find a bug in any code snippet or sample output:
1. Please open an issue using the [Wrong or Unclear Solution template](../../issues/new/choose).
2. Include the **smallest failing input** and the expected output verified by an independent brute-force script.

---

## Submitting Pull Requests

Before opening a Pull Request:

1. **Verify against brute force:** Every correction must be validated against a brute-force baseline across random inputs.
2. **Synchronize Python & C++:**
   - Always update both Python 3 and C++17 implementations in sync.
   - Ensure both solutions adhere to the same I/O format (e.g. read array size on first line, elements on second line).
3. **Preserve Section Structure:**
   Every problem file must preserve standard markdown sections:
   `Problem -> Sample Input/Output -> Constraints -> Key Insight -> Approach -> Python 3 -> C++ 17 -> Edge Cases`.
4. **Run Local Checks:**
   ```bash
   pip install pytest
   pytest -q tests/test_solutions.py
   python tests/compile_cpp.py
   ```
5. **No Copyright Infringement:** Do not copy problem descriptions verbatim from commercial platforms; paraphrase algorithmic core concepts and cite original references in `06-resources/sources.md`.
