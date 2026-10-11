---
name: go-errors
description: Apply the author's error handling conventions when writing, modifying, or reviewing Go code that creates or wraps errors.
---

# Go Errors

## Rules

- Prefer `github.com/pkg/errors` for creating and wrapping errors.
- When an operation returns an error, check `err != nil` and return `errors.Wrap(err, "additional_information")` with meaningful context about the failed operation.
- When a function returns only an error and no `err` variable is already available in the enclosing scope, prefer calling it in the `if` initializer with `if err := operation(); err != nil`.
- If `err` already exists in the enclosing scope, reuse it with `if err = operation(); err != nil`. Do not use `:=` to declare a new `err` that shadows the existing variable.
- Always write error message text in lowercase English. Use `snake_case` for multiword descriptions and identifier labels.
- Include relevant non-sensitive identifiers already available near the error, such as an order ID or job ID. Use `errors.Wrapf` when adding these values. Preserve identifier values as they are; the lowercase and `snake_case` rules apply to message text and labels.

## Examples

```go
import "github.com/pkg/errors"

if err != nil {
	return errors.Wrap(err, "load_config")
}
```

With a relevant non-sensitive identifier:

```go
if err != nil {
	return errors.Wrapf(err, "load_order order_id=%s", orderID)
}
```

For a new error:

```go
return errors.New("invalid_order_status")
```

Prefer a short declaration when no existing `err` needs to be reused:

```go
if err := userService.Update(u); err != nil {
	return errors.Wrapf(err, "update_user user_id=%s", u.ID)
}
```

Reuse an existing `err` rather than shadowing it:

```go
var err error
// Other operations may assign to err here.

if err = userService.Update(u); err != nil {
	return errors.Wrapf(err, "update_user user_id=%s", u.ID)
}
```
