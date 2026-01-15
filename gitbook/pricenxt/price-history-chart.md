# Price History Chart

The price history chart is the hero visualization on the Insight page. It blends historical spot/monthly prices, optional forecasts, confidence bandwidths, and delta badges so users can understand trajectory at a glance.

## Key Traits

- Built with `ReactECharts` plus shared primitives like `ChartContainer`, `ChartSettingsDropdown`, and `TimeRangeSelector`.
- Supports contextual interactions so users can toggle forecast/bandwidth layers and open the Price Details drawer without leaving the chart.

## Data Sources

- **Spot data** – `fetchSpotPriceData` (weekly). Loaded via React Query when the variant supports spot pricing.
- **Monthly data** – `fetchMonthlyPriceData` (month-open averages) for variants without spot coverage.
- **Variant context** – `useVariant` resolves localized naming and metadata for legends/tooltips.
- **Database contract** – rows reuse the `prices_with_delta` Postgres function type alias (`PriceRow`).

> **Tip**: Route date inputs through `toDbLocale` before hitting Supabase to avoid locale-related gaps.

## Interactive Controls

1. **Time range** – `TimeRangeSelector` maps to 12/24/36/48 data points via `getDataLimitFromRange`.
2. **Chart settings** – slideout checkboxes toggle forecast visibility, bandwidth envelopes, and average lines.
3. **Details drawer** – `PriceDetailsDrawer` surfaces metadata, commentary, and related cards without leaving the page.

## Visual Treatments

- Base series use brand gradients; forecast series switches to a dashed stroke defined in `CHART_COLORS.forecast`.
- Bandwidth is rendered through two stacked line series (`Band Min`, `Band Range`) so the filled area animates smoothly.
- `buildForecastAnnotation` inserts a mark line when forecast data exists, offsetting timestamps so the transition is natural.
- Custom tooltips format `change_abs`, `change_percent`, and analyst commentary into a styled panel using `createBadgeProps`.

## Axis and Scale Logic

- `computeYAxisBounds` pads min/max values by roughly 10% (or 100 currency units) to avoid clipping.
- Date ticks rely on `formatChartDateLabel` plus localized `toLocaleDateString`, so German and English tenants see appropriate labels.

## Integration Checklist

- Wrap the chart with `ChartContainer` to reuse loading and empty states from other insight components.
- Respect the active theme via `useTheme` + `getThemeColors`; both the palette and tooltip badges depend on it.
- When embedding under `/docs`, link back to the live Insight page so readers can immediately try the interactions.
