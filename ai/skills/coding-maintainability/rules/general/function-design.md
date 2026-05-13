# Function Design

## Core Rules

1. Use a single return point.
2. Prefer returning expressions directly over mutating a temporary result variable.
3. If an intermediate return value must be named, use the name result.
4. Avoid unnecessary braces in simple lambda expressions.
5. Keep control flow shallow and intention-revealing.
6. Do not throw exceptions for expected outcomes; model failure paths as typed return values instead.
7. Prefer returning `undefined` for expected errors unless distinguishing error causes is critical to caller behavior.
8. Do not assert or re-verify arguments in internal functions; fulfilling preconditions is the caller's responsibility.

## Shape Pattern

```ts
export function normalize(input: Input): Output {
	return (isSimple(input) ? transformSimple : transformComplex)(input)
}
```
## Review Prompts

1. Is there exactly one return statement?
2. Can branch logic be expressed as a direct return expression instead of mutable temporary state?
3. If an intermediate value is still necessary, is it named result?
4. Are side effects minimized and obvious?
5. Are failure paths represented in typed return values rather than `throw`?
6. For expected errors, is `undefined` used by default unless cause differentiation is required?
7. Is argument validation avoided in internal functions so preconditions are enforced by the caller?

## Agent Guardrail

Before finalizing any edit that changes a function body:

1. Re-scan each touched function and verify there is exactly one `return` statement.
2. If conditional flow is needed, use a local variable named `result` and return once at the end.
3. Reject patches that introduce early returns in edited functions, even when behavior remains correct.
