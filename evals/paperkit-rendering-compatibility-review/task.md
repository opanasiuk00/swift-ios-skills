# Markup Persistence Review

## Problem/Feature Description

A teammate proposed a first PaperKit persistence helper for an iOS document browser. It stores the serialized markup next to a PNG thumbnail so older app versions can still show something useful.

The proposal contains this rough thumbnail path:

```swift
let image = UIGraphicsImageRenderer(size: thumbnailSize).image { ctx in
    Task {
        await markup.draw(in: ctx.cgContext, frame: frame, options: options)
    }
}
try image.pngData()?.write(to: thumbnailURL)
toolPicker.maximumLinearExposure = 4
paperVC.markup = try PaperMarkup(dataRepresentation: data)
```

Review the plan and write the corrected guidance for the document team.

## Output Specification

Create a file named `paperkit-persistence-review.md` containing:

- A concise list of issues in the proposal.
- Corrected Swift snippets or pseudocode for safe thumbnail rendering and loading.
- Platform notes for insertion UI if the same codebase later adds Mac Catalyst and macOS targets.
