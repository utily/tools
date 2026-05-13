# Regex Safety

Avoid regex constructions that can become unbounded on crafted input.

## Required Style

- Prefer bounded and specific patterns.
- Avoid nested quantifier patterns that risk catastrophic backtracking.

## Review Checks

1. Could any regex become unbounded on adversarial input?
2. Can a safer parse strategy replace a risky regex?
