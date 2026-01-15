# Cards and Card Types

Cards are the atomic insight units that populate every board column. They encapsulate data fetching, formatting, and visualization logic behind a consistent API so users can mix and match analytics without touching SQL.

Each card instance stores:

1. **Title** – the label displayed on the card chrome.
2. **Metadata** – type-specific configuration captured via the card configurator (variant IDs, comparison lists, gauge thresholds, etc.).

```ts
export interface CardFormData<T extends CardMetadata = CardMetadata> {
  readonly title: string;
  readonly metadata: T;
}
```

## Lifecycle

1. The user opens the card configurator (`select → configure`).
2. The selected card type provides default metadata from the registry.
3. Validation (`CardFormValidation`) confirms required fields/variants are present.
4. On save, the card persists under the active column and renders through the card registry.

> **Tip**: Metadata objects are read-only to prevent accidental mutation. Clone before editing local state in forms.

## Card Types

| Type | Usage | Key metadata |
| --- | --- | --- |
| `price` | Track a single variant (spot or monthly) | `variantId`, `deltaPeriod`, `showForecast`, `chartStyle` |
| `delta` | Highlight period-over-period deltas | `variantId`, `deltaPeriod`, `showForecast` |
| `list` | Monitor multiple variants in a single list | `variantIds[]`, `deltaPeriod`, highlight color |
| `compare` | Compare up to four variants side by side | `variantIds[]`, `deltaPeriod` |
| `gauge` | Threshold-driven KPI views | `variantId`, `gauge { min, max, t1 }`, `chartStyle` |
| `spread` | Track spreads between two variants | `variantIds[]`, `deltaPeriod`, `calculationMode` |

All available IDs live in `CARD_TYPE_OPTIONS`, keeping filters, selectors, and Supabase enums aligned.

```ts
export const CARD_TYPE_OPTIONS = [
  { id: "price", labelKey: "board.filters.card-types.price" },
  // ...
];
```

## Categories and Status Badges

- **Categories** (`CardCategory`) cluster cards when browsing (commodity, capacity, arbitrage, currency, plastixx, news).
- **Status** (`CardStatus`) flags experimental or upcoming types (e.g., `coming-soon`), surfaced as Untitled UI badges in the configurator.

> **Callout**: Combine category + status metadata to drive feature-flag rollouts without branching the registry.

## Display vs. Preview Components

- `CardPreviewProps` power lightweight previews inside the configurator.
- `CardDisplayProps` render the live dashboard cards and receive optional `onEdit` handlers so users can relaunch the configurator with the same metadata.

Keeping these props aligned ensures cards render consistently across creation, duplication, and drag-and-drop flows.
