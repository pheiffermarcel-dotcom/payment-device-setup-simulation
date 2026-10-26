# Public time-study data candidate

`time_study_setup_durations.csv` is a publication-oriented extraction from the student-collected time-study workbook. **Release only after industry-partner authorisation and review of disclosure risks.**

- 120 observed work orders, 30 observations per device group (`EMV_G1`, `EMV_G2`, `NonEMV_G1`, `NonEMV_G2`).
- `ObservationID` is a newly generated within-group sequence identifier. It is **not** an original work-order or sales-order number.
- `BatchQuantity` is the observed number of devices in the batch.
- `S1_seconds` through `S7_seconds` are the *recorded* step durations in seconds. A blank means there was no recorded duration, not a zero-duration event. Non-EMV devices do not undergo S5 or S6.
- `RecordedTotal_seconds` is the total shown in the original observational workbook. It is not adjusted for OTA contamination or missing individual step observations.
- All observation dates, DSO identifiers, warehouse labels, start/end timestamps, operational notes, network spot tests and other potential identifying details have been omitted from this extraction.
- The underlying time studies informed the simulation inputs. **Not every recorded duration was used unchanged in model fitting**: in particular, S4 observations contaminated by OTA activities were excluded from relevant processing-time fits.
- Do not interpret the observations as representative of all future operating conditions. Personal differences between staff were not modelled through individual DSO-specific input distributions.

`model_inputs/` contains tables documented in the thesis. Some empirical values are rounded presentation numbers, not byte-exact executable model inputs; consult its README before attempting replication.
