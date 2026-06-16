# UIKit Images and Keyboard Handling

Use this reference for image memory, async cell image loading, keyboard
avoidance, and scroll-view behavior.

Official docs:

- `UIKeyboardLayoutGuide`: https://sosumi.ai/documentation/uikit/uikeyboardlayoutguide
- Keyboards and input: https://sosumi.ai/documentation/uikit/keyboards-and-input

## Contents

- [Image Memory](#image-memory)
- [Cell Image Loading](#cell-image-loading)
- [Keyboard Layout Guide](#keyboard-layout-guide)
- [Scroll Views](#scroll-views)
- [Checklist](#checklist)

## Image Memory

Decoded image memory is roughly `width * height * 4 bytes`. A compressed JPEG
can be small on disk but huge after decode. For thumbnails, downsample to
display size instead of loading full-size and resizing later.

## Cell Image Loading

Use cancel/clear/verify:

```swift
final class AvatarCell: UICollectionViewCell {
    private var representedID: User.ID?
    private var imageTask: Task<Void, Never>?

    override func prepareForReuse() {
        super.prepareForReuse()
        representedID = nil
        imageTask?.cancel()
        imageTask = nil
        imageView.image = nil
    }

    func configure(user: User, loader: ImageLoader) {
        representedID = user.id
        titleLabel.text = user.name

        imageTask = Task { [weak self] in
            guard let image = try? await loader.image(for: user.avatarURL) else { return }
            guard !Task.isCancelled else { return }
            await MainActor.run {
                guard self?.representedID == user.id else { return }
                self?.imageView.image = image
            }
        }
    }
}
```

## Keyboard Layout Guide

```swift
inputBar.snp.makeConstraints { make in
    make.horizontalEdges.equalTo(view.safeAreaLayoutGuide)
    make.bottom.equalTo(view.keyboardLayoutGuide.snp.top)
}

view.keyboardLayoutGuide.followsUndockedKeyboard = true
```

Use manual notifications only when supporting a platform path that lacks the
layout guide or when synchronizing custom animation state.

## Scroll Views

- Pin content to `contentLayoutGuide`.
- Pin scroll view frame to `frameLayoutGuide` or superview constraints.
- Avoid manually changing content inset and keyboard constraints at the same
  time unless the behavior is explicitly designed.
- Keep the focused field visible after layout updates.

## Checklist

- [ ] Large images are downsampled before display.
- [ ] Cell image tasks cancel in `prepareForReuse`.
- [ ] Cells clear stale images before new async work finishes.
- [ ] Async completion verifies the cell still represents the same model ID.
- [ ] Keyboard avoidance uses `UIKeyboardLayoutGuide` where available.
- [ ] Floating keyboard behavior is considered.
- [ ] Scroll view content and frame layout guides are constrained correctly.
