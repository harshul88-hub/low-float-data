# Low float stock data, free and live

A free, machine readable dataset of exchange listed US low float stocks, refreshed every
scan during market hours. Price, change on the day, volume, average volume, market cap
and float for roughly 600 names. No account, no API key, no rate limit.

**Dataset page and documentation:** https://ignitionalerts.com/dataset/

## Download

| Format | URL |
|---|---|
| CSV | https://ignitionalerts.com/assets/data/universe.csv |
| JSON | https://ignitionalerts.com/assets/data/universe.json |

Both files are rewritten on every scan while the market is open and freeze at the close.
Fetch the file rather than scraping the page, and please cache for a few minutes.

## Fields

| CSV column | JSON key | Meaning |
|---|---|---|
| ticker | t | Exchange listed US symbol |
| price | p | Last price in USD at the snapshot |
| change_pct | chg | Move on the day, percent. Blank above 400 percent (almost always an unrestated reverse split) |
| volume | vol | Shares traded so far today |
| avg_volume | avg | Three month average daily volume |
| market_cap | mcap | Market capitalisation in USD |
| float | flt | Shares available to trade. Blank when the provider figure exceeds shares outstanding |

A blank means the number was not trusted. It never means zero. Over the counter names and
anything under ten cents are excluded, because a name nobody can realistically trade does
not belong in a dataset about trading.

## Quick start

```python
import pandas as pd
df = pd.read_csv("https://ignitionalerts.com/assets/data/universe.csv")
tiny = df[df["float"] < 5_000_000].sort_values("change_pct", ascending=False)
print(tiny.head(10))
```

## Embed the live movers table on your own site

Two lines, nothing to sign up for. It renders instantly from data baked into the file and
refreshes on our side.

```html
<div id="ignition-screener"></div>
<script async src="https://ignitionalerts.com/assets/embed-screener.js"></script>
```

Options on the container: `data-rows="5"` to show fewer names, `data-theme="light"` for a
light background. Sets no global variables and only writes inside its own div.

## Live views of the same data

* Screener with filters and sorting: https://ignitionalerts.com/screener/
* What moved each market day, one page per day: https://ignitionalerts.com/today/
* RSS feed of the daily record: https://ignitionalerts.com/today/feed.xml
* Plain English definitions of every term: https://ignitionalerts.com/glossary/

## License

The data is released under [Creative Commons Attribution 4.0](https://creativecommons.org/licenses/by/4.0/).
Use it for anything, including commercial work. The one condition is attribution: credit
Ignition Alerts and link to https://ignitionalerts.com/dataset/. One line in a notebook or a
README is enough.

Suggested citation: Ignition Alerts, Low float universe dataset, https://ignitionalerts.com/dataset/,
accessed on the date you fetched it.

## Not advice

This is price and volume data. It recommends nothing. Low float and micro cap stocks are
among the most volatile securities in the market and total loss is possible.
