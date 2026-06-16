# UIKit Memory and Concurrency

Use this reference for retain cycles, delegates, timers, notification
observers, `Task` lifecycle, and main-actor UI updates.

## Contents

- [Ownership](#ownership)
- [Common Retain Cycles](#common-retain-cycles)
- [Task Lifecycle](#task-lifecycle)
- [Main Actor](#main-actor)
- [Checklist](#checklist)

## Ownership

View controllers should deallocate after dismissal/pop. During development, add
temporary `deinit` logging for screens with async work, timers, delegates, or
embedded controllers.

Default rules:

- Use `[weak self]` in escaping closures.
- Re-capture `[weak self]` in nested stored closures.
- Class-constrain delegate protocols and store delegates as weak.
- Invalidate timers/display links when the screen stops needing them.

## Common Retain Cycles

```swift
timer = Timer.scheduledTimer(withTimeInterval: 1, repeats: true) { [weak self] _ in
    self?.tick()
}

cell.onTap = { [weak self] id in
    self?.showDetail(id)
}

protocol PickerViewDelegate: AnyObject {
    func pickerViewDidSelectItem(_ view: PickerView, id: Item.ID)
}

final class PickerView: UIView {
    weak var delegate: PickerViewDelegate?
}
```

`CADisplayLink` retains its target. Use a weak proxy or invalidate it before
the view controller should deallocate.

## Task Lifecycle

```swift
private var loadTask: Task<Void, Never>?

override func viewDidAppear(_ animated: Bool) {
    super.viewDidAppear(animated)
    loadTask = Task { [weak self] in
        await self?.load()
    }
}

override func viewDidDisappear(_ animated: Bool) {
    super.viewDidDisappear(animated)
    loadTask?.cancel()
    loadTask = nil
}
```

After each `await`, check cancellation before updating UI:

```swift
let response = try await client.fetch()
guard !Task.isCancelled else { return }
apply(response)
```

## Main Actor

UIKit UI work must happen on the main actor. Detached work is not isolated:

```swift
Task.detached {
    let image = await decodeImage()
    await MainActor.run {
        imageView.image = image
    }
}
```

Avoid `DispatchQueue.main.sync`; it can deadlock.

## Checklist

- [ ] View controllers with async work deallocate after dismissal/pop.
- [ ] Escaping closures capture `self` weakly unless ownership is deliberate.
- [ ] Delegates are weak and protocols are `AnyObject` constrained.
- [ ] Timers/display links are invalidated.
- [ ] Screen-owned tasks are stored and cancelled.
- [ ] UI updates after `await` check cancellation where relevant.
- [ ] Detached tasks return to `MainActor` before touching UIKit.
