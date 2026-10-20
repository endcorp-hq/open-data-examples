# GPB05 uncertainty correction

Updated October 20, 2026. END corrected the retained GPB05 night-only uncertainty
field using policy `end-gpb05-analysis-error-zero-offset-v1`. This is an END correction based on the
[GHRSST L4 specification, section 9.3](https://ghrsst.github.io/GDS/l4.html#analysis-error)
and observed source encodings; it is not a NOAA-approved reprocessing.

The correction retains each original packed int16 value and missing mask, uses
zero offset with the source scale approximately 0.01 K, and retains the packed
valid range 0–500. Original source files are unchanged. Unknown encodings and
out-of-range values fail closed. No date cutoff is used because source offsets
reverted in early 2018.

All 4,402 retained error maps from June 2, 2014 through October 18,
2026 were rebuilt from ETag-pinned source files. All 114,099,840,000 packed
cells, including missing cells, matched their source hashes after the final
snapshot was reopened. Of those files, 1,316 had a nonzero offset and 3,086
already used zero. The repair changed only the error array; historical SST,
ice, masks, coordinates and timestamps remained intact.

A subsequent production replay of June 2, 2014 preserved its original nominal
time and every raw field without creating a duplicate date. Appending October
19 passed full error, SST and ice-field comparisons plus exact mask and
coordinate checks. The measured archive contains 4,403 unique dates
through October 19, 2026, with 120 retained calendar gaps.

The [verification ledger](gpb-error-correction.json) supplies the policy,
snapshot identifiers, per-date ETags and hashes, and replay measurements.
The [original audit](gpb-historical-validation.json) remains evidence of the
uncorrected snapshot, not the current archive's status.

These checks cover all historical error maps, while historical SST/ice data
were protected by the error-only diff. They do not claim every historical
field was compared to its source. Full public-export validation and hosting
setup remain launch requirements; there is no public dataset endpoint yet.
