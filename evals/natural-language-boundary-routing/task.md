# NaturalLanguage Boundary Routing

## Problem/Feature Description

A product team has one feature request:

- Scan text from a receipt image.
- Transcribe a spoken note.
- Tokenize and identify the language of the resulting text.
- Detect names and sentiment in the text.
- Find semantically similar keywords with embeddings.
- Optionally add a custom text classifier or word tagger.
- Translate a summary to Spanish.
- Localize UI strings with String Catalogs (`.xcstrings`), plural receipt item
  counts, right-to-left layout, and date/currency formatting.
- Maybe use Apple Intelligence to generate the summary.

Explain which parts belong in the NaturalLanguage skill and which should move
to sibling skills or frameworks.

## Output Specification

Create a file named `natural-language-boundary-routing.md` containing:

- A concise responsibility split by framework or sibling skill.
- The NaturalLanguage/Translation pieces that should stay in scope.
- The correct handoffs for OCR, speech transcription, UI localization, and
  generative summarization.
- Any availability or privacy caveats that affect the split.

Do not create an Xcode project. Keep the answer as implementation guidance and
snippets only.
