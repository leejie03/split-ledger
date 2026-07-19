# Ledger — split complex bills

A single-page web app for splitting bills where an even split isn't enough: uneven shares,
fractions, per-item quantities, and section-level reconciliation (discounts, tax, tip).

**Live:** https://leejie03.github.io/split-ledger/

No accounts, no backend — everything is one static `index.html` and saves in your browser.

## The model

Each cell is **the share of an item's price that a person pays**:

```
person's cost for an item  =  price × cell
```

- **Even split among N** → enter `1/N` in each person's cell (or hover the row and tap **÷**).
- **Quantities** → enter `2`, `1.5`, etc. (e.g. a ¥3.00 seat charge each → put `1` for everyone).
- **Uneven shares** → any fraction, e.g. `2/7`.
- **Didn't have it** → leave blank.

A section can be **reconciled** to the amount actually paid — useful when the receipt total
differs from the sum of shares (a discount, service charge, or tip). Every subtotal in that
section scales by `actuallyPaid ÷ computedTotal`.

Grand total per person = the sum of their reconciled section subtotals.

## Features

- Multiple people, sections, and items — all editable inline.
- Fraction / decimal / quantity input with a per-row **split-evenly** helper.
- Per-section **reconcile** to an actual paid amount.
- **Settle up**: enter who already paid; it computes who owes whom in the fewest transfers.
- Toggle each cell between the share you typed and the computed amount.
- **Multiple saved bills** (new / duplicate / rename / delete), all stored locally.
- **Export**: copy a plain-text summary, download a CSV, or copy a shareable link
  (the whole bill is encoded in the URL — opening it offers to import a copy).
- Light / dark / auto theme.

## Type

Set in [Inter](https://rsms.me/inter/) (self-hosted variable font, SIL Open Font License),
with tabular figures (`tnum`) and open digits (`ss01`).

## Develop

It's a static file — open `index.html` in a browser, or serve the folder:

```sh
python3 -m http.server 8000   # then visit http://localhost:8000
```

Hosted on GitHub Pages from the `main` branch root.
