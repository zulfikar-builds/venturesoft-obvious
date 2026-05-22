---
applies_to: "**/*.py"
description: "Python-specific code review rules for Autobuild's review agent."
---

# Python Code Review Overlay

This overlay defines quality gates for Python code review. Rules are grouped by category and severity. The review agent should flag violations and block merge for **Critical** and **High** severity issues.

---

## Type Safety — `HIGH`

- Flag any function (including methods) missing parameter type annotations.
- Flag any function missing a return type annotation; `-> None` must be explicit.
- Flag overuse of `Any` — every `Any` requires a justification comment; prefer specific types or `TypeVar`.
- Flag `cast()` calls that circumvent the type system without a comment explaining why.
- Require type stubs (`py.typed` marker or inline annotations) for all public API surfaces.
- Flag `# type: ignore` without an inline explanation.

---

## Error Handling — `HIGH`

- Flag bare `except:` — always catch a specific exception type.
- Flag `except Exception:` that does not re-raise or log the exception.
- Flag empty `except` blocks (swallowed exceptions) — at minimum log and re-raise.
- Require `raise NewException(...) from original` when chaining exceptions to preserve context.
- Flag `except` clauses that catch and silently discard errors in background threads or async tasks.

---

## Security — `CRITICAL`

- Flag hardcoded secrets, API keys, tokens, or passwords in source files — use env vars or a secrets manager.
- Flag any call to `eval()`, `exec()`, or `compile()` with dynamic or user-controlled input.
- Flag SQL queries built via string interpolation (`f"SELECT ... {value}"`) — require parameterized queries.
- Flag `pickle.loads()` applied to untrusted data — unsafe deserialization.
- Flag `yaml.load()` without `Loader=yaml.SafeLoader` — use `yaml.safe_load()` instead.
- Flag `subprocess.call(..., shell=True)` or `subprocess.run(..., shell=True)` when the command includes user input.
- Flag use of `os.system()` with dynamic input.
- Flag `tempfile.mktemp()` (insecure) — use `tempfile.mkstemp()` or `tempfile.NamedTemporaryFile()`.

---

## Testing — `MEDIUM`

- Flag new or modified public functions with no corresponding test coverage.
- Flag tests that only cover the happy path — expect at least one edge case (empty input, boundary value, error path).
- Expect `pytest`-style tests (plain functions + fixtures); flag `unittest.TestCase` subclasses in new test files.
- Flag tests that mock so heavily they no longer test real behaviour.
- Flag test functions without assertions — a test that always passes is not a test.

---

## Imports — `MEDIUM`

- Flag wildcard imports (`from module import *`) in non-`__init__.py` files.
- Flag wildcard imports in `__init__.py` unless explicitly re-exporting a public API.
- Flag circular imports — restructure into a shared module or use lazy imports.
- Prefer absolute imports over relative imports (`from mypackage.utils import x` vs `from ..utils import x`).
- Flag unused imports not covered by the linter (e.g. imports guarded by `TYPE_CHECKING` that are used at runtime).

---

## Performance — `MEDIUM`

- Flag N+1 query patterns in ORM code — use `select_related` / `prefetch_related` (Django) or equivalent.
- Flag `time.sleep()` inside `async def` functions — use `await asyncio.sleep()` instead.
- Flag synchronous I/O (`open()`, `requests.get()`, etc.) inside `async def` without a thread executor.
- Flag unnecessary list materialisation where a generator or iterator suffices (e.g. `list(x for x in ...)` passed only to `for`).
- Flag repeated attribute lookups inside tight loops — hoist to a local variable.

---

## Python Idioms — `LOW`

- Flag mutable default arguments (`def f(items=[])`, `def f(config={})`) — use `None` sentinel + guard.
- Flag late-binding closures in loops that capture loop variables by reference inside `lambda` or nested functions.
- Flag `type(x) == SomeClass` for type checking — use `isinstance(x, SomeClass)`.
- Flag manual iteration over a range just to index a list (`for i in range(len(xs))`) — use `enumerate(xs)`.
- Flag `dict()` / `list()` / `set()` constructors where a literal (`{}`, `[]`, `set()`) is clearer.
- Flag string concatenation inside loops — use `"".join()` instead.
- Flag `if x == True:` / `if x == False:` — use `if x:` / `if not x:`.

