# Econ 3916 PS1: The Cost of Living Brief

## Finding

This household's cost of living rose about **21%** from 2019 to 2024
(Laspeyres index 120.6, 2019 = 100). Something that cost $100 in 2019
would cost about $121 in 2024.

The household is a two-earner family in Florida with one school-aged child,
commuting by public transit. Rent is almost half the budget and rose 20%,
so it accounts for 9.6 of the 20.6 points of increase. Childcare and
utilities rose the most (25% each) but are a small share of spending.

The increase is below the national figures for the same period: headline
CPI rose about 23% and national rent about 27%, mainly because this
household's rent grew more slowly than the national average.

## How robust is it?

I swept each category's weight from 0 to 0.5, rescaling the others in
proportion. If any one spending share were off by 10 percentage points,
the index would stay between about 120.1 and 121.1. Only an extreme shift,
such as moving one category to half the budget, pushes it to 118–123.

**Confidence: high** that the true increase is close to 21%.

## Caveats

- The Laspeyres index assumes the household kept buying the same basket.
  If they cut back on items that became more expensive, the true increase
  is slightly lower.
- October 2025 CPI data is missing because of the federal government
  shutdown. This does not affect the 2019–2024 comparison.

## Files

- `Econ_3916_PS1.ipynb`: the full analysis (basket, FRED series,
  sample audit, seasonal adjustment check, weight sensitivity).
