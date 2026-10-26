# Frozen simulation input tables

The CSV files reproduce the tables reported in Appendix C of the 2026 thesis. They have been prepared from the project's LaTeX source rather than from operational systems.

- `processing_time_parameters.csv` gives the 24 final setup-step inputs. Parameter meanings depend on distribution: lognormal uses natural-log-space mean and standard deviation, while Weibull and Gamma use shape and scale. Model A represents a total work-order duration and Model B a per-device duration multiplied by work-order quantity.
- `empirical_processing_observations_rounded.csv` reproduces 30 observations for each of two empirical distributions. **These are rounded presentation values, not the unrounded data sampled in the simulation.** Do not substitute this CSV as a byte-exact simulation input.
- `ota_parameters.csv` reproduces the reported frozen OTA values. The Wi-Fi-given-OTA probability is an operational estimate, and the derived OTA requirement probability is not a directly observed incidence.
- `ota_affected_quantity_observations.csv` reproduces the 24 recorded OTA affected-quantity observations used as an empirical pool. These observations were derived from a distinct eligible subset from the Wi-Fi incidence estimate.

The files contain no work-order or sales-order identifiers. Their public release still requires confirmation of the industry partner's permissions. The native `.spp` files remain the authoritative executable model configurations.
