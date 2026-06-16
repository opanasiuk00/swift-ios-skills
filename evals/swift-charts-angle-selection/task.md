# Swift Charts Angle Selection Review

## Problem/Feature Description

Review this donut chart selection model:

```swift
@State private var selectedProduct: String?

Chart(products, id: \.name) { item in
    SectorMark(angle: .value("Sales", item.sales))
        .foregroundStyle(by: .value("Product", item.name))
        .opacity(selectedProduct == nil || selectedProduct == item.name ? 1 : 0.4)
}
.chartAngleSelection(value: $selectedProduct)
```

The team expects tapping a sector to select its product name, but the code
behaves poorly and is hard to type-check.

## Output Specification

Create `angle-selection-review.md` with:

- What is wrong with the binding model.
- The corrected selection state type.
- How to map the selected angle back to a product/category.
- Any pie/donut readability caveats that should stay in the implementation.
