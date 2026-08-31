# MBA 561 — Retail Transactions and Weather

Data and analysis notebook for the MBA 561 final project. The project joins store
transaction records to daily high temperatures and looks at whether weather relates
to sales volume and revenue.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/JishanAhmed2019/mba_561_data/blob/main/FinalProject.ipynb)

## Getting started

Click the badge above. It opens the notebook in Colab and everything runs from there —
no downloads, no Google Drive, no path changes.

The first code cell clones this repository into the Colab session, so the data is
available to every group member at the same path:

```python
!git clone https://github.com/JishanAhmed2019/mba_561_data.git
DATA_DIR = "/content/mba_561_data/"
```

To run it locally instead, clone the repo and set `DATA_DIR` to the folder path on
your machine. You will need `pandas`, `numpy`, `matplotlib`, and `pyarrow`.

## Files

| File | Description |
|---|---|
| `FinalProject.ipynb` | The analysis notebook (Tasks 0–10) |
| `ities.parquet` | Transaction line items, 438,151 rows × 13 columns |
| `max_temp.xz` | Weekly high temperatures for 2016, 52 rows × 9 columns |

## About the data

**`ities.parquet`** — one row per item sold. Columns include `Date`, `OperationType`
(SALE or RETURN), `LineItem`, `Department`, `Category`, `StoreNumber`,
`TransactionNumber`, `CustomerCode`, `Price`, `Quantity`, and `TotalDue`. Dates run
from 2014-01-04 to 2017-04-05. `Price` and `TotalDue` are each missing 12 values.
Returns are recorded as negative amounts.

**`max_temp.xz`** — a pickled DataFrame compressed with xz, read with
`pd.read_pickle()`. One row per week of 2016, with `Week`, `WeekStarting`, and seven
columns holding the daily high temperature in degrees Fahrenheit. Every
`WeekStarting` value falls on a Sunday. No missing values.

Note that the two files overlap only in 2016, so the joined dataset is limited to
that year.

## Analysis steps

1. Load both files and inspect their structure
2. Convert the date columns to `datetime`
3. Summary statistics and missing-value handling
4. Aggregate transactions to the daily level
5. Reshape the weather data from wide to long and build a calendar date
6. Join the two datasets on date
7. Scatter plots of temperature against revenue and quantity

## Working on this together

Saving from Colab (**File → Save a copy in GitHub**) commits the whole notebook at
once, so two people saving the same file will overwrite each other. Coordinate who
is editing before you push.

Run **Runtime → Restart and run all** before saving. Colab stores outputs inside the
file, and a notebook that ran out of order will show results nobody can reproduce.
