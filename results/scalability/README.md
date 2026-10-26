# Scalability experiment — 24 demand–DSO configurations

This directory contains the final replication-level exports for a complete **4 × 6 experimental design**, with demand multipliers **15, 20, 25 and 30** and Device Support Officer (DSO) capacities **5–10**.

- **24 configurations** and **2,898 final replication observations**.
- Independent terminating simulation replications with variable numbers of observations per configuration.
- Primary response: mean Sales Order Setup Lead Time (**SOSLT**), evaluated per replication.
- All 24 configurations meet the study's relative 95% confidence-interval half-width target of at most **1%**, based on the provided final exports.

## File contents

- `scalability_replications.csv`: combined, machine-readable replication-level data from all 24 final scenario exports. Contains **2,898 data rows** and the original **22 measures/identification columns**.
- `scalability_summary.csv`: calculated sample sizes, mean SOSLT, standard deviations, 95% Student-t confidence intervals, relative half-widths, mean DSO utilisation and prepared-demand coverage.
- `scenario_file_manifest.csv`: identifies each final scenario Excel file, its original uploaded filename, row count and original KPI column label.
- `scenario_exports/`: the **24 original final Excel exports**, retained for traceability. One misleading filename has been corrected in this publication copy.

## Replications per scenario

| Demand multiplier | 5 DSOs | 6 DSOs | 7 DSOs | 8 DSOs | 9 DSOs | 10 DSOs |
|---|---:|---:|---:|---:|---:|---:|
| 15x | 123 | 128 | 56 | 110 | 48 | 69 |
| 20x | 224 | 81 | 104 | 123 | 45 | 108 |
| 25x | 239 | 141 | 133 | 83 | 60 | 53 |
| 30x | 270 | 180 | 209 | 130 | 80 | 101 |

## Interpretation and units

- `DemandMultiplier` represents the simulated compression of historical work-order releases, not a physical count of orders.
- `NumberOfDSOs` is the simulated Device Support Officer capacity.
- `MeanSOSLT` values in the replication-level CSV are **numeric seconds**. The summary also provides `MeanSOSLT_hms` as `h:mm:ss.ssss`.
- Other model time totals are also stored as numeric seconds in the replication-level exports.
- Utilisation and coverage columns are fractions (e.g. `0.5` = 50%).
- Original spreadsheets for the first 12 configurations use the older header `MeanTimeToClient` for column five. The consolidated file standardises it to `MeanSOSLT`, consistent with the revised thesis KPI. Retained original Excel exports are **not altered internally**.

## Source-file clarifications

- The uploaded `D30_DSO5_172Reps.xlsx` actually contains **270** consecutive replication records, with its mean matching the 270-replication thesis result. The publication copy is renamed `D30_DSO5_270Reps.xlsx`. The manifest preserves the original filename for traceability.
- The extra `D15_DSO5_12Reps.xlsx` is just the first 12 rows of `D15_DSO5_123Reps.xlsx` and is excluded to avoid duplicates.
- The two workbooks called `ExperimentManagerResultsandDetailedResults_Scalability.xlsx` and `ExperimentManagerResultsandDetailedResults_Scalability2.xlsx` are earlier Experiment Manager reports/exports and are excluded from these final data products.
- The initial 10-replication pilots and superseded runs are **not appended** to the final replication data.

## Validation and reproducibility notes

Every final scenario has consecutive, unique replication numbers beginning at 1 and no missing data cells in the 22 exported columns. For every replicate, pre-updated devices used plus unupdated devices used equal **4,893**, and prepared devices minus prepared devices used equal ending prepared inventory. These checks validate the exported accounting identities, **not** full simulation verification or independent operational validation.

The full design supports demand–capacity response comparisons. Any statistical comparisons should be recalculated on these 24 final samples, rather than reusing 12-scenario Welch ANOVA / Games–Howell results. Use variance-aware methods when required by the data.

The public release of the source `.spp` models and any work-order time-study records remains subject to the industry partner's permission and anonymisation requirements. This folder includes **replication-level simulation KPIs**, not individual customer or order identifiers.
