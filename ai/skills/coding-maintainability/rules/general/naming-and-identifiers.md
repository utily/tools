# Naming and Identifiers

## Core Rules

1. Do not abbreviate names except for: UI, Id, max, min.
2. Prefer descriptive names over short names.
3. Prefer single-word identifiers when clarity is preserved.
4. Use single-letter identifiers only within a very tight local span.
5. Use consistent domain terms across files and modules.
6. Prefer natural, stable ordering for grouped names and members when no stronger domain order exists.
7. Keep naming style team-oriented and consistent rather than author-specific.

## Do

- Use names like accountNumber, reportHeader, countryCode.
- Keep naming symmetric for conversion methods, for example: from, to, parse.

## Forbidden

- Unclear aliases such as acc, hdr, cfg, tmp when a domain term exists.
- Introducing alternate terms for the same concept in nearby files.
