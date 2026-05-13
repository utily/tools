# Validation Style

## Core Rules

1. Treat all external input as untrusted until explicitly validated.
2. Validate input before usage, never after business logic has already consumed it.
3. Escape or encode user-provided values before using them in redirect targets, callback targets, generated HTML, or query construction.

## Review Prompts

1. Is any external input consumed before validation?
2. Are user-provided values encoded before entering output or transport contexts?
3. Are boundary validations explicit and local to the boundary?
