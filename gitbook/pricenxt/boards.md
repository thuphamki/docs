# Boards Overview

Boards organize the insights users care about inside the Pricenxt dashboard. Each board belongs to a user or workspace and contains a set of ordered columns, and every column holds cards that display price intelligence, comparisons, or alerts.

> **Note**: Boards are usually the first surface users see after logging in. Column order and content density directly influence perceived value.

## Board Anatomy

- **Columns** – ordered swimlanes (e.g., Watchlist, Active Deals, Completed). Users can collapse them to reduce noise.
- **Cards** – self-contained widgets (price deltas, spreads, lists, comparisons) that inherit their rendering logic from the Cards registry.

### Columns

- Persisted in the Supabase `columns` table and loaded through `fetchBoard`.
- Store `order`, `name`, and `is_collapsed` so personalization survives reloads.
- Support collapse/expand via the `onToggleCollapse` handler exposed on `KanbanProps`.

### Cards Inside a Column

- Saved as nested records within each column result from the same Supabase query.
- Sorted by the `order` field so drag-and-drop operations translate into deterministic layouts.
- Include a `type` and `metadata` payload to tell the Cards pipeline which component to mount and how to configure it.

## Data Lifecycle

1. `fetchBoard(boardId)` fetches a board plus nested columns/cards in one Supabase call.
2. The response is normalized into the `KanbanColumn` / `KanbanProps` structure before rendering.
3. Reordering, collapsing, or editing cards emits an `onChange` payload so React Query mutations can persist updates back to Supabase.

```ts
interface KanbanColumn<T> {
  id: string;
  columnId: string;
  title?: string;
  items: T[];
  order?: number;
  isCollapsed?: boolean;
}
```

> **Tip**: Use discriminated unions for card payloads so every card component receives a fully typed metadata object.

## Interaction Guidelines

- **Drag and drop** – always update stored `order` values before persisting; avoid relying on array indexes.
- **Column density** – keep each column to roughly eight cards for readability; encourage additional boards instead of overloaded columns.
- **Collapsing** – synchronize `isCollapsed` between client state and Supabase so collaborators see consistent layouts.
- **Empty states** – show instructional placeholders (e.g., “Drop a card here”) when a board or column has no cards yet.

## When to Create a New Board

Create separate boards when teams need different commodity mixes or regions, distinct workflows (procurement vs. sales), or when future sharing boundaries require isolation. Keeping concepts scoped to specific boards also makes the `/docs` embed more actionable for end users.
