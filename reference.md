# Comment formats by language

Use the format that matches the target file's language. If the language is not below, keep the file's existing comment style or use that language's standard doc format.

---

## JavaScript / TypeScript

**Block:** JSDoc `/** ... */` above function/class.

```javascript
/**
 * Short description.
 * @param {string} id - User id
 * @returns {Promise<User>}
 * @example
 * await fetchUser('u1')
 */
async function fetchUser(id) { ... }
```

- File header: `/** @file overview in one line */` or multi-line `/** ... */`.
- Inline: `//` for single line.
- **TypeScript**: prefer TSDoc tags (`@remarks`, `@typeParam`) when the project uses TSDoc; otherwise fall back to JSDoc. Do not restate types already in the signature.

---

## Python

**Block:** Docstring `"""..."""` (triple double-quote). Prefer one style per file; match the existing style if present.

- **Google style**: `Args:`, `Returns:`, `Raises:` sections.
- **NumPy style**: section headers with dashes (`Parameters`, `Returns`, `Raises`).
- **Sphinx / reST style**: `:param name:`, `:returns:`, `:raises:`.

```python
def fetch_user(user_id: str) -> User:
    """Fetch user by id.

    Args:
        user_id: The user's unique id.

    Returns:
        User instance.

    Raises:
        NotFoundError: When user does not exist.
    """
```

- Module: docstring at top of file.
- Class: docstring under `class` line.
- Inline: `#` for single line.

---

## Java

**Block:** Javadoc `/** ... */` above class/method.

```java
/**
 * Fetches user by id.
 *
 * @param userId the user id
 * @return the user, or null if not found
 */
public User fetchUser(String userId) { ... }
```

- Class/interface: Javadoc above declaration.
- Inline: `//` or `/* ... */`.

---

## Kotlin

**Block:** KDoc `/** ... */` (Javadoc-style, supports `@param`, `@return`, `@see`).

```kotlin
/**
 * Fetches user by id.
 * @param userId The user id
 * @return [User] or null
 */
fun fetchUser(userId: String): User? { ... }
```

- Inline: `//` or `/* ... */`.

---

## C#

**Block:** XML doc comments `///` with tags like `<summary>`, `<param>`, `<returns>`.

```csharp
/// <summary>
/// Fetches user by id.
/// </summary>
/// <param name="userId">The user id</param>
/// <returns>The user or null</returns>
public User FetchUser(string userId) { ... }
```

- Inline: `//` or `/* ... */`.

---

## Go

**Block:** Full-sentence comment above declaration; first word is the name (e.g. "FetchUser fetches...").

```go
// FetchUser returns the user for the given id, or nil if not found.
func FetchUser(ctx context.Context, id string) (*User, error) {
```

- Package: one comment above `package` (e.g. `// Package pkg does ...`).
- Inline: `//`.

---

## Rust

**Block:** Doc comment `///` for item below; `//!` for enclosing item (e.g. module).

```rust
/// Fetches the user by id.
///
/// # Errors
/// Returns error when the user is not found.
pub fn fetch_user(id: &str) -> Result<User> {
```

- Inline: `//`.

---

## C / C++

**Block:** Doxygen-style `/** ... */` or `///` with `@param`, `@return`, etc.

```c
/**
 * Fetches user by id.
 * @param id User id
 * @return User pointer or NULL
 */
struct User* fetch_user(const char* id);
```

- Inline: `//` or `/* ... */`.

---

## Ruby

**Block:** Above method/class; often YARD with `@param`, `@return`.

```ruby
# Fetches user by id.
#
# @param id [String] user id
# @return [User, nil]
def fetch_user(id)
```

- Inline: `#`.

---

## PHP

**Block:** DocBlock `/** ... */` with `@param`, `@return`, `@throws`.

```php
/**
 * Fetches user by id.
 *
 * @param string $id User id
 * @return User|null
 * @throws NotFoundException
 */
function fetchUser(string $id): ?User {
```

- Inline: `//` or `#`.

---

## Swift

**Block:** Xcode-style `///` or `/** ... */` with `- Parameter`, `- Returns`.

```swift
/// Fetches user by id.
/// - Parameter id: User id
/// - Returns: User or nil
func fetchUser(id: String) -> User? {
```

- Inline: `//`.

---

## Objective-C

**Block:** Same as C; above method use `/** ... */` with `@param`, `@return`.

```objc
/**
 * Fetches user by id.
 * @param userId The user id
 * @return User instance or nil
 */
- (User *)fetchUserWithId:(NSString *)userId;
```

- Inline: `//` or `/* ... */`.

---

## SQL

- Single line: `--`.
- Block: `/* ... */`.
- Prefer short comment above a statement or inline for non-obvious logic.

---

## Shell (Bash / Sh)

- Single line: `#`.
- No standard "doc block"; use `#` lines above function.

```bash
# Fetches user by id. Usage: fetch_user <id>
fetch_user() { ... }
```

---

## HTML / XML

- Block: `<!-- comment -->`.
- No standard doc format; use brief comments above sections or components.

```html
<!-- Navigation bar — collapses on mobile -->
<nav class="navbar">...</nav>
```

---

## CSS / SCSS / Less

- Block: `/* comment */`.
- SCSS and Less also support inline `//`.
- Prefer a short comment above each major section or non-obvious rule.

```css
/* Main layout — uses CSS Grid with 12-column system */
.container { ... }
```

---

## Dart

**Block:** Dartdoc `///` above declaration; supports `[]` for cross-references.

```dart
/// Fetches user by [id].
///
/// Returns `null` if the user is not found.
Future<User?> fetchUser(String id) async { ... }
```

- Library: `///` or `library` doc at top of file.
- Inline: `//`.

---

## Lua

- Single line: `--`.
- Block: `--[[ ... ]]`.
- No standard doc format; LDoc (`---`) is common in larger projects.

```lua
--- Fetches user by id.
-- @param id string User id
-- @return User or nil
function fetch_user(id) ... end
```

---

## Scala

**Block:** Scaladoc `/** ... */` (similar to Javadoc); supports `@param`, `@return`, `@throws`.

```scala
/**
 * Fetches user by id.
 * @param userId the user id
 * @return the user, or None if not found
 */
def fetchUser(userId: String): Option[User] = { ... }
```

- Inline: `//` or `/* ... */`.

---

## YAML

- Single line: `#` (no block comment syntax).
- Prefer brief inline comments for non-obvious values.

```yaml
timeout: 30  # seconds; matches upstream API SLA
```

---

## Unlisted languages

Use the **existing comments in the file** as the format. If there are none, use that language's common documentation style (e.g. Lua, Scala, R) and keep it consistent.
