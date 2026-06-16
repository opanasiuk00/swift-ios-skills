# Swift 6.3 Wiki Corrections

## Problem/Feature Description

A team wiki page about Swift 6.3 interoperability and performance annotations was drafted from memory. The maintainer wants a corrected note with enough code to prevent future copy-paste errors in systems-facing Swift modules.

## Output Specification

Create `swift63-interop-corrections.md` containing:

- A corrected version of the note.
- Minimal Swift examples for the corrected forms.
- A short explanation of why each draft claim was wrong.

## Draft Note

```markdown
Use `@c func export(_ bytes: UnsafeBufferPointer<UInt8>) -> Int32` when exporting a Swift function directly to C.

Use `@specialize(where T == Int)` to force a specialization of a generic function.

`@inline(always)` is only an optimization hint and may be ignored.

When two modules define the same symbol, write `ModuleName.symbol` to choose one.
```
