# Module and Export Style

## Core Rules

1. Organize by concept, not by utility grab-bags.
2. Keep module boundaries explicit and predictable.
3. Re-export internal modules intentionally through stable entry points.
4. Prefer named exports for clarity and refactor safety.
5. Use a natural and repeatable ordering of exported members when no stronger reason applies.
6. Decouple modules so each abstraction can be reasoned about in isolation.

## Common Pattern

- Import internal modules with underscore aliases when they are re-exported.
- Re-export through namespace in repositories that use namespace-based APIs.

## Example Pattern

```ts
import { Header as _Header } from "./Header"

export namespace Account {
	export import Header = _Header
}
```

## Review Prompts

1. Is each export part of a coherent public API?
2. Are import and re-export patterns consistent across siblings?
3. Could this module be split by concept for better readability?
4. Is export ordering stable and predictable for maintainers?

