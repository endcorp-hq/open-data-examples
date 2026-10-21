# GAMSSA historical gap recovery

On October 21, 2026, END recovered seven GAMSSA dates from the
[Australian Ocean Data Network](https://thredds.aodn.org.au/thredds/catalog/IMOS/SRS/SST/ghrsst/L4/GAMSSA/catalog.html):
August 27, 2008; September 15 and November 6, 2014; September 18, 2020;
August 17 and November 22, 2023; and December 15, 2024.

NASA’s current PO.DAAC collection omits these seven analysis dates. AODN has the
original ABOM files, with the same GAMSSA product ID, grid, timestamps, packing
and GHRSST free/open notice. END checked every source field against its declared
range and retained the original files with verified checksums.

The recovered archive contains 6,664 unique dates from July 23, 2008 through
October 20, 2026, with no missing calendar days. END inserted the recovered
rows in date order on an isolated Icechunk branch, checked every rewritten
packed value after each of 219 monthly commits, then reopened the final
snapshot and checked all monthly hashes again. A further source comparison
covered all 28 recovered SST, error, sea-ice and mask maps before promotion.
The normal converter then appended October 20 on the same branch. END checked
the new row against its original source and verified that existing values in
the affected chunks were unchanged.
Existing values, coordinates, packing and missing-value masks were preserved.
Recovered historical times retain the source’s noon timestamp. Recent rows
follow the existing converter’s calendar-day convention: October 20 is stored
at midnight. The ledger records both the source analysis time and stored time.

The verified snapshot is `VR0TJTFVT52HKC2RCMH0`. The
[source and verification ledger](gamssa-historical-recovery.json) records
file URLs and hashes, NASA search results, per-field checks and monthly hashes.

The sea-ice field remains absent on March 26–30, May 6 and September 23, 2026.
END checked AODN’s copies of all seven files too; none contains
`sea_ice_fraction`. These cells remain missing, as documented in the
[coverage inventory](coverage.json).

This recovery updates END’s operational archive. Public hosting and anonymous
release checks are still pending.
