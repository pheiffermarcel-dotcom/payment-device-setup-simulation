# Payment-device setup simulation

**Discrete-event simulation of payment-device setup and alternative preparation and work-allocation policies**  
Final-year BEng Industrial Engineering project · Stellenbosch University · 2026

## Project overview

This project develops discrete-event simulation (DES) models of the payment-device setup process undertaken by an industry partner. The analysis compares advance preparation, work-order allocation policies and resource-capacity scenarios without intervening in the live operation.

The work uses **Siemens Tecnomatix Plant Simulation 2404** and SimTalk. The analysed historical workload comprises **376 sales orders (SOs), 555 work orders (WOs), 4,893 devices and five Device Support Officers (DSOs)**. The study boundary covers applicable setup activities **S1–S7**, including conditional over-the-air (OTA) updates. Quality control, packaging, dispatch, reverse logistics and commercial activation are outside the modelled scope.

The principal outcome is **Sales Order Setup Lead Time (SOSLT)**, measured from the earliest recorded WO creation timestamp for an SO until setup completion of its last constituent WO. SOSLT is not full delivery time or customer activation time.

## Repository contents

| Path | Contents |
|---|---|
| [`models/`](models/) | Five native `.spp` models (requires Plant Simulation) |
| [`simtalk/`](simtalk/) | 195 exported SimTalk methods, grouped by model |
| [`data/time_study_setup_durations.csv`](data/time_study_setup_durations.csv) | 120 work-order-level time-study observations without dates, personnel IDs or notes |
| [`data/model_inputs/`](data/model_inputs/) | Reported processing and OTA input tables, including clearly marked rounded data |
| [`results/scalability/`](results/scalability/) | 24-scenario replication data, summaries, source export manifest and Excel exports |

## Simulation models

| Model | File | Role |
|---|---|---|
| As-Is | [`As_Is.spp`](models/As_Is.spp) | Baseline with historically assigned DSOs and conditional setup logic |
| To-Be 1 | [`To_Be_1.spp`](models/To_Be_1.spp) | Advance device preparation during idle DSO capacity, retaining historical customer-WO assignment |
| To-Be 2 | [`To_Be_2.spp`](models/To_Be_2.spp) | To-Be 1 plus hybrid/dynamic customer-WO assignment across available DSOs |
| To-Be 3 | [`To_Be_3.spp`](models/To_Be_3.spp) | To-Be 2 with a revised, demand-normalised preparation-group selection policy |
| Scalability | [`ScalabilityModel.spp`](models/ScalabilityModel.spp) | Varies historical WO release intensity and DSO capacity to examine scaling behaviour |

Each `.spp` file is the native Plant Simulation artefact. The `simtalk/` folders contain text exports for inspection, not independently runnable programs.

### Exported SimTalk source

| Folder | Methods |
|---|---:|
| [`simtalk/As_Is/`](simtalk/As_Is/) | 23 |
| [`simtalk/To_Be_1/`](simtalk/To_Be_1/) | 42 |
| [`simtalk/To_Be_2/`](simtalk/To_Be_2/) | 43 |
| [`simtalk/To_Be_3/`](simtalk/To_Be_3/) | 43 |
| [`simtalk/ScalabilityModel/`](simtalk/ScalabilityModel/) | 44 |
| **Total** | **195** |

Methods shared between models are included within each respective model folder to preserve an inspectable record.

## Time-study data

The [`data/time_study_setup_durations.csv`](data/time_study_setup_durations.csv) file records **120 observed WOs**, 30 each for EMV Grade 1, EMV Grade 2, non-EMV Grade 1 and non-EMV Grade 2. It preserves observed device quantities and recorded S1–S7 durations (seconds), including missing values. No original SO/WO IDs, dates, employee identifiers, start/end clock timestamps or operational field notes are included.

These are *observational measurements*, not necessarily the same processed inputs used directly by the executable simulation. Some measurements, including S4 observations affected by OTA activity, were excluded from relevant fitted processing-time inputs. See [`data/README.md`](data/README.md) and [`data/model_inputs/README.md`](data/model_inputs/README.md).

## Historical operating-policy comparison

Four configurations were compared under the same historical WO workload: As-Is and Models To-Be 1, 2 and 3. In the historical scenarios, **Model To-Be 2 reduced mean SOSLT by 19.34% (33.67 minutes)** relative to As-Is. This was accompanied by approximately **428.7 additional hours of modelled DSO work**, associated with advance preparation. The modelled reduction is not a measured improvement in live operating performance, and simulated DSO work is not automatically equivalent to additional paid hours.

## Scalability results

The [`results/scalability/`](results/scalability/) directory provides the final experiment, crossing demand-release multipliers **15, 20, 25 and 30** with **5–10 DSOs**. The resulting **24 configurations** contain **2,898 final independent simulation replications**, with varying replication counts per scenario. The reported primary-response 95% confidence-interval relative half-width is at most **1%** in all 24 cases.

| File | Description |
|---|---|
| [`scalability_replications.csv`](results/scalability/scalability_replications.csv) | All 2,898 replication-level observations and KPI columns |
| [`scalability_summary.csv`](results/scalability/scalability_summary.csv) | Sample sizes, mean SOSLT, standard deviations, confidence intervals and supporting response means |
| [`scenario_file_manifest.csv`](results/scalability/scenario_file_manifest.csv) | Maps the 24 final scenarios to source export filenames and rows |
| [`scenario_exports/`](results/scalability/scenario_exports/) | The 24 final source `.xlsx` exports retained for traceability |
| [`README.md`](results/scalability/README.md) | Column units, scenario-specific sample sizes and data reconciliation notes |

Demand multipliers compress historical release intervals. They are **simulation stress-test settings**, not forecasts of future customer demand. The experiments assume continuously available DSOs rather than actual working shifts.

### Reproducibility limitation

The exported [`mExportScalabilityResults.txt`](simtalk/ScalabilityModel/mExportScalabilityResults.txt) reflects an earlier **12-scenario, 10-replication** export configuration. For the final 24-configuration experiment, the export routine was manually adapted to accommodate differing replication counts. Those exact intermediate export configurations are **not fully preserved in this one source text file**. The final scenario exports and manifest record the data analysed for the project. Therefore, the repository should not be described as a fully automated, one-click reproduction of every final run.

The native models may depend on embedded historical input tables and software settings. A compatible Siemens Plant Simulation installation and licence are required to open and execute them.

## Verification, validation and limitations

Simulation implementation was verified. Validation was assessed against observed S1–S7 processing evidence, including an aggregate time-study-derived reference; this is not independent predictive validation because the observations also informed the fitted processing-time inputs. Independent operational timestamps were unavailable for directly validating SOSLT.

The conclusions are conditional on the historical data, excluded Grade 3 work, processing-input assumptions, conditional OTA representations and continuously available modelled DSO resources.

## Data privacy and rights

The industry partner is not identified in this publication. **Public release of the native model files and simulation data must be authorised by the industry partner, and all files should be checked for embedded confidential records before changing repository visibility.** The cleaned time-study CSV removes known identifying metadata from the source workbook, but this does not constitute a guarantee against re-identification.

No public reuse or redistribution licence is provided for the models, source code or datasets. Access through a public repository does not imply permission to redistribute or reuse proprietary material. Siemens Tecnomatix Plant Simulation is proprietary software belonging to its respective owner.

## Research context

Stellenbosch University · Department of Industrial Engineering · BEng Industrial Engineering · 2026. Research conducted with an industry partner.
