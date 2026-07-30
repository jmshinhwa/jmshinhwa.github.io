---
title: Build a HELOC Credit-Line Calculator in a Spreadsheet
keyword: heloc loan calculator
tags: ['heloc loan calculator', 'tools', 'spreadsheet']
category: tools
lang: en
---

# Build a HELOC Credit-Line Calculator in a Spreadsheet

A HELOC calculator is three numbers and one subtraction, but almost every online version hides the arithmetic behind a lead form. Here is the whole sheet, cell by cell, so you can rebuild it in Google Sheets or Excel in about five minutes and keep it.

## Why it reduces to one calculation

The only thing that decides your credit line is the lender’s combined loan-to-value cap. Multiply the appraised value by that cap, subtract what you still owe on the first mortgage, and the remainder is what the lender can offer. Everything else on a HELOC quote is downstream of that one line.

## The input cells

Put these on a sheet named `Inputs`. The values shown are the ones used in the worked example further down, so you can check your sheet against it.

| Cell | What it holds | Example value |
| --- | --- | --- |
| `B2` | Home appraised value | 450000 |
| `B3` | Current 1st mortgage balance | 220000 |
| `B4` | Lender max CLTV (0.85 = 85%) | 85% |
| `B5` | Amount you plan to draw | 60000 |

## The formulas

These go on a second sheet named `Equity & Credit Line`. They are reproduced from the formula graph of a workbook we build and ship, back-translated to spreadsheet notation — the dependency order below is the order they evaluate in, so enter them top to bottom.

**`B4`** — Estimated HELOC credit line available  
```
=((Inputs!B2 * Inputs!B4) - Inputs!B3)
```

**`B6`** — Credit line left unused after draw  
```
=(((Inputs!B2 * Inputs!B4) - Inputs!B3) - Inputs!B5)
```

## Worked example

With the input values in the table above, the sheet produces:

| Result | Value |
| --- | --- |
| Estimated HELOC credit line available | `$162,500` |
| Credit line left unused after draw | `$102,500` |

If your sheet returns these numbers from those inputs, every formula is entered correctly. If one is off, the dependency order is the usual cause — an intermediate cell that has not been entered yet reads as zero.

## Notes from building it

Two things worth knowing once the sheet works. A cap is a ceiling, not a promise — income and credit can pull the offer below it. And if the subtraction comes out negative, that is the sheet telling you the first mortgage already uses the whole cap, which is real information, not an error.

The workbook this was reconstructed from has 9 input cells and 6 result cells; the 4 inputs and 2 results above are the ones that carry the decision. A filled-in copy is free here: [heloc loan calculator workbook](https://getreadystack.com/m/heloc-loan-calculator-1098c0-starter).
