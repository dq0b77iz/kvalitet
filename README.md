# Kvalitet

A small data quality monitor that runs entirely in the browser. It's built along the same lines as tools like Validio: profile the source data first, then watch it with validators that learn what normal looks like.

## What it does

- **Source profile:** column types, missing values, distinct counts, ranges, top values and distributions.
- **Validators:** row count, missing values, mean and duplicate checks. Each one can be split by a segment column (for example, market) and use either a dynamic threshold (a band learned from the trailing 14 days) or fixed min/max limits.
- **Incidents:** every value that falls outside its expected range, newest first, with severity and how far it is from normal.
- **Freshness:** how long since each segment last received new rows.
- **Your own data:** upload a CSV and Kvalitet profiles it and suggests a starting set of validators.

## Sample data

The page opens with a synthetic `warehouse.orders` table: five markets (SE, NO, DK, FI, US) over 60 days. A few problems are planted so the validators have something to catch:

- Norway order volume drops to about a third for two days
- Denmark is missing `customer_id` on roughly 23% of orders for two days
- Finland's `amount_sek` stops converting from EUR, so average order value falls about 90%
- 14 duplicate order IDs in Sweden on one day
- Denmark stops sending data, which the freshness check flags

## Running it

It's a single static `index.html` with no build step and no backend. Open it in a browser, or serve it with GitHub Pages.
