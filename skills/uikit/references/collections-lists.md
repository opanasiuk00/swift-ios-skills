# UIKit Collections and Lists

Use this reference for `UICollectionView`, `UITableView`, diffable data
sources, compositional layouts, cell registration, and reusable cell behavior.

Official docs:

- Updating collection views using diffable data sources: https://sosumi.ai/documentation/uikit/updating-collection-views-using-diffable-data-sources
- `UICollectionViewCompositionalLayout`: https://sosumi.ai/documentation/uikit/uicollectionviewcompositionallayout
- `UIListContentConfiguration`: https://sosumi.ai/documentation/uikit/uilistcontentconfiguration-swift.struct

## Contents

- [Modern Stack](#modern-stack)
- [Stable Identity](#stable-identity)
- [Cells](#cells)
- [Performance](#performance)
- [Checklist](#checklist)

## Modern Stack

For new non-trivial list/grid screens, prefer:

- `UICollectionViewDiffableDataSource`
- `NSDiffableDataSourceSnapshot`
- `UICollectionViewCompositionalLayout`
- `UICollectionView.CellRegistration`
- `UIContentConfiguration` and `UIBackgroundConfiguration`

## Stable Identity

Snapshot item identifiers should be stable IDs, not large mutable value models:

```swift
struct User: Identifiable, Hashable {
    let id: UUID
    var name: String
    var avatarURL: URL?
}

typealias DataSource = UICollectionViewDiffableDataSource<Section, User.ID>
typealias Snapshot = NSDiffableDataSourceSnapshot<Section, User.ID>
private var usersByID: [User.ID: User] = [:]
```

Use `reconfigureItems(_:)` when visible content changes but identity and cell
type stay the same.

## Cells

```swift
let registration = UICollectionView.CellRegistration<UICollectionViewListCell, User.ID> {
    [weak self] cell, indexPath, id in
    guard let user = self?.usersByID[id] else { return }

    var content = cell.defaultContentConfiguration()
    content.text = user.name
    content.secondaryText = user.avatarURL?.host()
    cell.contentConfiguration = content
}
```

For reusable cells:

- Reset transient UI in `prepareForReuse`.
- Cancel image/network tasks in `prepareForReuse`.
- Do not store index paths as identity.
- Keep callbacks weak or delegate-based to avoid retaining controllers.
- Prefer value configuration methods over exposing many mutable subviews.

## Performance

- Avoid `reloadData()` for routine updates.
- Apply snapshots from a single serialized UI path.
- Use prefetching for network/image-heavy lists.
- Keep cell hierarchies shallow.
- Avoid deeply nested stack views in high-volume cells.
- Use estimated sizes carefully; self-sizing requires a complete constraint
  chain from top to bottom and leading to trailing.

## Checklist

- [ ] Diffable item identifiers are stable IDs.
- [ ] Snapshot has no duplicate identifiers.
- [ ] `CellRegistration` is used instead of string reuse identifiers.
- [ ] Content/background configurations are used for standard list cells.
- [ ] Cells cancel async work and reset state on reuse.
- [ ] Small content changes use `reconfigureItems`, not full reloads.
- [ ] Layout uses compositional layout for mixed sections, grids, or carousels.
