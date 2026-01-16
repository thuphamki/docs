# Price History Chart

The price history chart is the hero of every Insight page. It blends historical spot or monthly prices, optional forecasts, confidence bandwidths, and delta badges so you can understand trajectory at a glance.

## What the Chart Shows

- Historical **spot** or **monthly** prices (depending on what the selected variant supports).
- Optional **forecasts** that extend the line forward so you can see where analysts expect the trend to go.
- A **bandwidth envelope** that hints at the optimistic and pessimistic scenarios.
- Compact **delta badges** that spell out how much the price moved over the window you selected.

Everything is updated live, so you can trust it in meetings and exports.

## Reading the Layers

- **Solid line**: actual traded or published prices. Hover any point to see the exact value and the time stamp in your locale.
- **Dashed line**: forecasted values. They always start where the historical data ends.
- **Shaded band**: the lighter area around the line shows the potential range. A wider band means more volatility or uncertainty.
- **Badges above the chart**: summarize the absolute and percentage move versus the previous period so you do not have to calculate it yourself.

> **Tip:** When the dashed line and the solid line overlap, use the legend to temporarily hide the forecast so you can focus on just the historical movement.

## Controls You Can Use

1. **Time range** – switch between 12, 24, 36, or 48 data points to zoom in on recent action or pull back for context.
2. **Chart settings** – open the slider menu to toggle forecast, bandwidth, or the rolling average line on or off.
3. **Details drawer** – click *Price details* to open commentary, methodology, and related cards without leaving the page.

Each change updates the chart instantly, making it easy to test a scenario while someone is asking the question.

## Data Sources in Plain Language

- If the product trades frequently, you will see **weekly spot prices**.
- If it only settles monthly, the chart switches to **month-open averages** so there are no gaps.
- Localized product names ensure legends, tooltips, and exports all use the same label your team expects.

No manual formatting is needed—the system automatically handles currencies, locales, and number precision.

## Visual Cues That Help Storytelling

- The y-axis always includes a buffer so the line never touches the frame, making presentations easier to read.
- Date labels automatically translate to the language set in your profile (e.g., German vs. English).
- Forecast sections include a subtle divider line to show where assumptions start, so stakeholders can see what is confirmed history versus projected.

Use these cues when narrating the chart: “Everything left of the divider is realized. Right of it is our forecast band.”

## Sharing Tips

- Screenshot or export right after toggling the layers you care about. The chart remembers your choices until you refresh.
- Pair the chart with a board card if you want the same view inside a column—cards reuse the identical data pipeline.
- Add a link back to the live Insight page whenever you drop the chart into a doc so readers can interact with the controls themselves.
