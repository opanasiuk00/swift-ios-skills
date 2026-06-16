A recipes app is adding App Intents support so recipes can appear in Spotlight, Siri, and Shortcuts. The current proposal is:

- Make `RecipeEntity` conform to `IndexedEntity`.
- Add `@Property(title:)` and `@Property(summary:)` annotations for searchable metadata.
- Build a custom `attributeSet` from scratch for every recipe.
- Index the same recipes with both `CSSearchableIndex.default().indexAppEntities(recipes)` and the app's existing `CSSearchableItem` indexing pipeline.
- Rebuild the index on every launch.
- Use integer database row IDs as entity IDs.
- Open recipe results by relying on the app's ordinary launch screen to infer the right route.

Write a concise review and corrected implementation sketch. Call out which parts are correct, which parts should change, and the production indexing lifecycle you would recommend.
