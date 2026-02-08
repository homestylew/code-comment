# Examples

## 1. Good vs bad (redundant comment)

**Bad** — comment only repeats the code:

```javascript
// set x to 5
let x = 5;
// call getData
const data = getData();
```

**Good** — comment explains why or non-obvious contract:

```javascript
// Default retry count for transient errors (see API SLA)
let x = 5;
// Response is cached for 60s; invalidate after mutation
const data = getData();
```

---

## 2. Good vs bad (noise)

**Bad** — every line commented with no added meaning:

```python
def total(items):
    s = 0          # set s to 0
    for x in items:  # loop over items
        s += x      # add x to s
    return s       # return s
```

**Good** — one docstring is enough for obvious logic:

```python
def total(items):
    """Sum numeric values in items. Items must be numeric."""
    s = 0
    for x in items:
        s += x
    return s
```

---

## 3. Response follows user language (i18n)

**User says (Chinese):** "给这段加一下注释"

**Correct:** Add comments in **Chinese** (match user's message).

```javascript
/**
 * 根据用户 id 拉取用户信息，未找到时返回 null
 * @param {string} id - 用户 id
 * @returns {Promise<User|null>}
 */
async function fetchUser(id) { ... }
```

**User says (English):** "Add comments to this"

**Correct:** Add comments in **English** (or match existing file language).

---

## 4. Response follows detail level

**User says:** "简单注释一下" / "brief comments only"

**Correct:** Only file/function summary, minimal inline.

```python
"""本模块提供用户拉取与缓存。"""

def fetch_user(uid: str) -> User:
    """根据 uid 拉取用户。"""
    ...
```

**User says:** "详细注释" / "add detailed comments"

**Correct:** Doc block + inline for branches and non-obvious steps.

```python
"""本模块提供用户拉取与缓存。"""

def fetch_user(uid: str) -> User:
    """根据 uid 拉取用户；本地缓存未命中时请求 API。"""
    # 先查本地缓存，避免重复请求
    cached = _cache.get(uid)
    if cached is not None:
        return cached
    # 调用下游 API，失败时抛出 NetworkError
    ...
```

---

## 5. Scope follows selection

- User **selects one function** and asks for comments → comment **only that function** (and its params/return), do not rewrite the whole file.
- User says **"整个文件"** / **"whole file"** → add file-level comment + all exported functions/classes as appropriate.

---

## 6. Good vs bad (type redundancy)

**Bad** — comment restates types already in the signature:

```typescript
/**
 * @param id - string, the user id
 * @returns Promise<User | null>
 */
async function fetchUser(id: string): Promise<User | null> { ... }
```

**Good** — comment adds semantics, skips type info already visible:

```typescript
/**
 * Fetches user from remote API with local cache fallback.
 * @param id - Unique user identifier (UUID v4)
 * @returns The user, or null if not found
 */
async function fetchUser(id: string): Promise<User | null> { ... }
```

---

## 7. File-level and class-level comments

**File-level** — brief module summary at top of file:

```java
/**
 * User service — handles user CRUD and permission checks.
 * Depends on {@link UserRepository} and {@link AuthService}.
 */
package com.example.service;
```

**Class-level** — describes responsibility and key behavior:

```java
/**
 * Manages user lifecycle: creation, lookup, deactivation.
 * Thread-safe; backed by a concurrent cache.
 */
public class UserService {
    ...
}
```

---

## 8. Handling existing comments

**Before** — file already has an outdated comment:

```python
def connect(host: str, port: int) -> Connection:
    """Connect to server."""
    # retry 3 times
    for attempt in range(5):
        ...
```

**After** — update inaccurate comment, keep accurate ones, add missing doc:

```python
def connect(host: str, port: int) -> Connection:
    """Establish connection to the given server with retry.

    Args:
        host: Server hostname or IP.
        port: Server port number.

    Raises:
        ConnectionError: After all retry attempts fail.
    """
    # Retry up to 5 times with exponential backoff
    for attempt in range(5):
        ...
```

---

## 9. Detailed comments for complex logic

**User says:** "详细注释" / "add detailed comments"

```go
// ProcessOrder validates, charges, and fulfills the given order.
// Returns ErrInvalidOrder if items are empty or total is non-positive.
func ProcessOrder(ctx context.Context, order *Order) error {
	// Validate order integrity before any side effects
	if len(order.Items) == 0 {
		return ErrInvalidOrder
	}
	total := calculateTotal(order.Items)
	if total <= 0 {
		return ErrInvalidOrder
	}

	// Attempt payment; abort early on failure to avoid partial fulfillment
	if err := chargePayment(ctx, order.UserID, total); err != nil {
		return fmt.Errorf("payment failed: %w", err)
	}

	// Mark as paid before shipping — if shipping fails,
	// the reconciliation job will detect the mismatch and retry
	order.Status = StatusPaid
	if err := shipOrder(ctx, order); err != nil {
		order.Status = StatusPaymentOnly
		return fmt.Errorf("shipping failed: %w", err)
	}

	order.Status = StatusFulfilled
	return nil
}
```
