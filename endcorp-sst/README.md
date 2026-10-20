# END Sea Surface Temperature Collections

Dataset documentation, updated October 20, 2026. END converts six upstream
sea surface temperature (SST) collections into versioned, cloud-readable Zarr V3
arrays using Icechunk. The upstream agencies produce the analyses; END maintains
the conversion, quality metadata and access examples.

**Public data release pending.** This repository provides documentation and a
tutorial for a planned public release. There is no public END dataset endpoint
yet. Publication depends on hosting setup, source-rights checks and release
validation. This page does not announce an active AWS sponsorship or Registry
listing. The proposed scope is the six collections below; OSTIA remains excluded until
historical redistribution rights are confirmed.

## Collections and measured coverage

Coverage is a dated measurement, not an assertion that every intervening
calendar date exists. GPB05 was refreshed on October 20 and reaches October 19;
other rows retain the October 19 inventory through October 17.

| Collection | Producer | Nominal grid | Earliest stored date | Latest stored date | Unique dates | Missing calendar dates |
| --- | --- | --- | --- | --- | --- | --- |
| CMC V2 | Canadian Meteorological Centre | 0.2° | 1991-09-01 | 2017-03-17 | 9,330 | 0 |
| CMC V3 | Canadian Meteorological Centre | 0.1° | 2016-01-01 | 2026-10-17 | 3,943 | 0 |
| GAMSSA | Australian Bureau of Meteorology | approximately 28 km | 2008-07-23 | 2026-10-17 | 6,654 | 7 |
| GPB05 night | NOAA Office of Satellite Products and Operations | approximately 5 km | 2014-06-02 | 2026-10-19 | 4,403 | 120 |
| OISST V2.1 | NOAA National Centers for Environmental Information | 0.25° | 1981-09-01 | 2026-10-17 | 16,483 | 0 |
| OSTIA | UK Met Office | 0.05° | 2007-01-01 | 2026-10-17 | 7,206 | 24 |

CMC V2 is historical. The operational scheduler checks the active feeds four
times daily; upstream availability determines new data arrival. Recent source
files can be preliminary and can later be revised. A published release must
identify a fixed snapshot so an analysis remains reproducible after revisions.

The [coverage inventory](coverage.json) records measured date coverage, complete
missing-date lists, coordinate groups, array layouts and known field gaps. It is
a dated pre-release inventory, **not a download manifest**. Stored array attributes
can contain partial historical notes; `known_source_field_gaps` is the explicit
field-level ledger, separate from `missing_calendar_dates` for absent whole days.
Physical release size and object count will be published with the first release.
The October 20 [operational capacity measurement](capacity.json) counts 297.96 GB
across 2,260,980 current objects, including repository history, before the GPB05
repair added new history. This is a sizing
baseline, not the eventual public release size; noncurrent object versions and
Bronze/Gold are excluded. The annualized recent-modification estimate is a
planning scenario, not measured net growth.

## Storage and discovery

The planned public layout is `data/<collection>.icechunk/`, `metadata/` and
`docs/`. A release manifest will supply the bucket, region, repository prefix,
immutable snapshot, group and coverage for each collection. Public endpoint and
snapshot fields are deliberately unset until destination validation is complete.

An Icechunk repository contains metadata, snapshots, manifests and chunks. Open
it through Icechunk, then pass a read-only session to Xarray. A raw S3 mapping
of an `.icechunk/` directory is not a standalone Zarr store. All referenced chunks
must be readable anonymously before a release is advertised.

## Fields and decoding

| Field | Collections | Meaning and decoded units |
| --- | --- | --- |
| `sst` | OISST | SST in Celsius |
| `anom` | OISST | Source-provided SST anomaly in Celsius; retain the upstream climatology definition |
| `err` | OISST | Estimated error standard deviation in Celsius |
| `ice` | OISST | Source sea-ice concentration; inspect retained units and packing before interpretation |
| `analysed_sst` | Other five collections | SST in Kelvin; subtract 273.15 after CF decoding for Celsius |
| `analysis_error` | Other five collections | Error standard deviation in Kelvin; temperature differences do not need the 273.15 conversion |
| `sea_ice_fraction` | Other five collections | Sea-ice area fraction, dimensionless after decoding |
| `mask` | Other five collections | Source-specific flags; interpret `flag_values`, `flag_masks` and `flag_meanings` |
| `preliminary` | Where present | Source revision state for a date; absence is not proof that a date is final |
| `crs` | GAMSSA | Coordinate reference metadata |

Coordinates are `time`, `lat`, `lon`, plus the singleton `zlev` dimension for
OISST. Xarray decodes CF scale/offset and missing values. Do not apply packing
a second time. Compare decoded values rather than raw packed integers across
products. The inventory preserves exact per-array attributes; source products
are not interchangeable and can estimate different SST definitions.

## Quality limits

- CMC V3 has four excess rows across three duplicate calendar dates; OISST has
  one excess row; OSTIA has duplicate dates and overlapping coordinate groups.
  For a single group, select the last stored row for each exact timestamp, then
  sort by date. Never concatenate overlapping OSTIA groups without an explicit
  coordinate and precedence policy.
- OSTIA contains two coordinate-signature groups and a legacy 40-day root.
  Select the group covering the requested date and grid. The release publisher
  must resolve overlapping partitions before advertising a combined view.
- GAMSSA sea-ice fields were absent upstream on March 26–30, May 6 and September
  23, 2026. Those cells carry the source fill sentinel and decode as missing;
  no sea-ice measurements were invented.
- GPB05 uncertainty has been corrected under an explicit END zero-offset
  policy. All 4,402 historical error maps were rebuilt from pinned source files
  and verified after reopening. Historical replay and the October 19 append
  passed, producing 4,403 unique dates. This is an END correction, not a
  NOAA-approved reprocessing. Public-export validation remains a launch gate.
- Calendar gaps listed in the inventory are absent from the retained source
  inventory too. A complete conversion is not a guarantee of gap-free upstream
  observations. Do not fill gaps implicitly.

The [GPB05 correction report](gpb-error-correction.md) records full historical
error-field verification and production replay. The [original audit](gpb-historical-validation.json)
records the earlier uncorrected snapshot and its sampled SST comparisons.

## Reader and tutorial

The [tutorial notebook](get-to-know-a-dataset.ipynb) opens a fixed
OISST snapshot, selects a week in the equatorial Pacific, plots SST and computes
a latitude-weighted regional anomaly. It also reports preliminary status and
missing values. It defaults to anonymous access and deliberately requires the
final public destination to be configured. The notebook never silently falls
back to local AWS credentials.

Use Python 3.12 and the accompanying [requirements](requirements.txt).
These versions match the qualified conversion environment. See the official
[Icechunk storage guide](https://icechunk.io/en/latest/guides/storage/) and
[Zarr documentation](https://zarr.readthedocs.io/en/stable/) for format details.
Compute can run locally or in a user's own AWS account near the hosting region.
The sponsored account hosts data; it is not the tutorial compute environment.

## Attribution and support

The [source rights and citation guide](source-rights.md) identifies each producer,
product and applicable policy. Cite the original product and version, access date
and END release snapshot. END provides format conversion; the originating
agencies remain the scientific data producers.

Report conversion, documentation and access problems through
[GitHub issues](https://github.com/endcorp-hq/open-data-examples/issues). Include
the collection, public release snapshot, selected dates/region, dependency
versions and a minimal example. Never include credentials. Source science
questions should go to the original product provider. END maintains these
examples and the conversions; no response-time or availability SLA is offered.

END-authored example code and documentation use the [MIT license](../LICENSE).
Upstream datasets and retained source metadata keep their own terms; MIT does
not relicense them. Public endpoint configuration and anonymous execution will
be completed when the first validated release is available.
