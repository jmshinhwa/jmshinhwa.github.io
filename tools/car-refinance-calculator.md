---
title: Car Refinance Break-Even in a Spreadsheet: the PMT Formula That Decides It
keyword: car refinance calculator
tags: ['car refinance calculator', 'tools', 'spreadsheet']
category: tools
lang: en
---

# Car Refinance Break-Even in a Spreadsheet: the PMT Formula That Decides It

Whether refinancing a car is worth it comes down to one comparison: how much the monthly payment drops versus what closing costs. Both sides are one formula each. This page gives you the sheet that answers it, including the PMT call most write-ups skip.

## Why it reduces to one calculation

PMT is the whole trick. Give it the monthly rate, the number of months and the amount financed and it returns the new payment. Subtract that from the payment you make today and you have the monthly saving. Divide the closing costs by that saving and you have the month the refinance starts making you money instead of costing you.

## The input cells

Put these on a sheet named `Inputs`. The values shown are the ones used in the worked example further down, so you can check your sheet against it.

| Cell | What it holds | Example value |
| --- | --- | --- |
| `B2` | Current payoff balance from your lender (call them, don't trust the app's 'balance') | 18450 |
| `B4` | Current monthly payment, principal and interest only (leave out insurance) | 516 |
| `B6` | New APR you've actually been quoted (use the lowest real offer, not an ad) | 6.29% |
| `B7` | New loan term in months (36, 48, 60, 72) | 48 |
| `B8` | Closing costs: title, lien recording, doc fee, plus any prepayment penalty | 185 |

## The formulas

These go on a second sheet named `Payment & Savings`. They are reproduced from the formula graph of a workbook we build and ship, back-translated to spreadsheet notation — the dependency order below is the order they evaluate in, so enter them top to bottom.

**`B2`**  
```
=(Inputs!B6 / 12)
```

**`B3`**  
```
=PMT('Payment & Savings'!B2, Inputs!B7, (-Inputs!B2))
```

**`B4`** — Monthly payment drop  
```
=(Inputs!B4 - 'Payment & Savings'!B3)
```

**`B6`** — Months until the closing costs pay for themselves  
```
=IF(('Payment & Savings'!B4 <= 0), 999, ROUND((Inputs!B8 / 'Payment & Savings'!B4), 1))
```

## Worked example

With the input values in the table above, the sheet produces:

| Result | Value |
| --- | --- |
| Monthly payment drop | `$80.24` |
| Months until the closing costs pay for themselves | `2.30` |

If your sheet returns these numbers from those inputs, every formula is entered correctly. If one is off, the dependency order is the usual cause — an intermediate cell that has not been entered yet reads as zero.

## Notes from building it

One guard to build in: if the payment drop is zero or negative there is no break-even at all, so the sheet should say so rather than divide by a number near zero and print a confident-looking result. The IF wrapper below does that.

The workbook this was reconstructed from has 9 input cells and 6 result cells; the 5 inputs and 2 results above are the ones that carry the decision. A filled-in copy is free here: [car refinance calculator workbook](https://getreadystack.com/m/car-refinance-calculator-6e9955-starter).
