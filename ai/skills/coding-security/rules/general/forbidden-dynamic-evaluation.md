# Forbidden Dynamic Evaluation

Dynamic string evaluation is not allowed.

## Forbidden Patterns

- eval
- Function constructor with dynamic source
- setTimeout with string payload
- setInterval with string payload

## Review Checks

1. Could this code execute source text from strings?
2. Are timer calls function-based rather than string-based?
