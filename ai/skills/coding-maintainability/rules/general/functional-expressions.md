# Functional Expressions

Prefer expression-oriented functional flow over mutable statement chains when readability is preserved.

## Required Style

- Prefer direct return expressions for branch selection when clear.
- Use mutable temporary state only when it improves clarity.

## Review Checks

1. Can mutable temporary state be replaced by a direct return expression without reducing clarity?
2. Is control flow explicit enough for a teammate to safely modify later?
