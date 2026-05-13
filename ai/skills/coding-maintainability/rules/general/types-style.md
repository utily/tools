# Types Style

## Core Rules

1. Prefer explicit TypeScript types for public interfaces and function boundaries.
2. Pair exported domain types with runtime validation patterns when available.
3. Keep type names descriptive and domain-specific.
4. Use namespace grouping where the repository follows that pattern.

## Interface Pattern

- Exported types are commonly paired with type, is, and flawed bindings.
- Namespace wrappers are used to colocate related members.

## Example Pattern

```ts
export interface Account {
	number: Account.Number
	label?: Label
}
export namespace Account {
	export import Number = _Number
	export const { type, is, flawed } = isly.object<Account>({
		number: Number.type,
		label: Label.type.optional(),
	}).bind()
}
```

## Review Prompts

1. Are boundary inputs typed intentionally?
2. Are optional properties modeled intentionally?
3. Is type naming consistent with domain language?
