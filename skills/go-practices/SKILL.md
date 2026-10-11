---
name: go-practices
description: Apply the author's shared programming practices when writing, modifying, or reviewing Go code.
---

# Go Practices

Template. The example below does not represent the author's confirmed preferences.

## Rules

<!-- Add rules for package structure, naming, and error handling here. -->

## Example Rule

When returning an error, add context about the operation and preserve the original error with `%w`:

```go
return fmt.Errorf("load config: %w", err)
```
