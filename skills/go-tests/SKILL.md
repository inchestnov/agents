---
name: go-tests
description: Apply the author's testing style when writing, modifying, or reviewing Go tests.
---

# Go Testing Style

Template. The example below does not represent the author's confirmed preferences.

## Rules

<!-- Add rules for naming, organizing test cases, assertions, and mocks here. -->

## Example Test

```go
func TestSum(t *testing.T) {
	got := Sum(2, 3)
	if got != 5 {
		t.Fatalf("Sum(2, 3) = %d, want 5", got)
	}
}
```
