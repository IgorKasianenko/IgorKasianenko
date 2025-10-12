# 2025-10-12

## 🐍 TIL: Python Scope Tricks (`nonlocal` vs. Mutability vs. `self.`)

When writing recursive class methods in Python, for example in trees or dfs, you often need to update a maximum result variable defined in the outer scope. Python offers three main ways to handle this, each with trade-offs regarding **explicitness** and **readability** (the Zen of Python):

| Approach | Declaration | Update (Inside `dfs`) | Pros & Cons |
| :--- | :--- | :--- | :--- |
| **1. Mutable Container** | `res = [-float('inf')]` | `res[0] = max(res[0], ...)` | **Pro:** No `nonlocal` needed. **Con:** Requires a list (or dict) to hold a single value; less readable. |
| **2. `nonlocal` Keyword** | `res = -float('inf')` | `nonlocal res`; `res = max(res, ...)` | **Pro:** Explicitly rebinds the outer variable. **Con:** Only works for non-global enclosing scopes; less common than class attributes. |
| **3. Instance Attribute** | `self.res = -float('inf')` | `self.res = max(self.res, ...)` | **Pro:** **Most Pythonic in a class.** Clean, explicit, and standard way to manage state. |

**Zen of Python Verdict:**

For methods within a class, using **`self.res`** is the cleanest and most idiomatic solution. It uses standard object-oriented state management, aligning with "Explicit is better than implicit" and "Readability counts."

The mutable container (`res = []`) is a clever hack that works, but it's **implicit** and makes the code slightly harder to read. Use **`nonlocal`** only when you cannot use a class attribute and must reassign an immutable variable within a nested function.

### The Zen of Node Checks

In Python, checking for a null tree node should be simple and idiomatic:

$$\text{Preferred: } \quad \texttt{if not root:}$$

This is simpler and more readable than `if root is None`, as the `None` check is the only expected "falsy" value for a node object. This follows the Zen of Python's preference for simplicity and readability.