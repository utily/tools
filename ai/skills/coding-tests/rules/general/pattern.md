# Pattern

Example pattern for table-driven and single-case tests:

```ts
describe("DomainType", () => {
  it.each([
    { input: "input1", expected: true },
    { input: "input2", expected: false },
  ])("is $input", ({ input, expected }) => expect(domain.is(input)).toBe(expected))

  it("single case", () => expect(domain.from("A")).toBe("B"))
})
```
