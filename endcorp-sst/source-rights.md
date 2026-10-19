# Source rights and citation guide

Updated October 19, 2026. END converts the source analyses into versioned Zarr V3
and Icechunk storage. The original agencies remain the data producers. The
repository's MIT license covers END-authored examples and documentation; it
does not replace upstream data terms or retained source notices.

## Products and citations

Use the linked product record for the complete citation, scientific references
and current access conditions. Include the source version and your access date.

| END collection | Producer and product | Product reference |
| --- | --- | --- |
| `cmc_v2` | Canadian Meteorological Centre, GHRSST CMC 0.2° global foundation SST, version 2.0 | [Product record](https://podaac.jpl.nasa.gov/dataset/CMC0.2deg-CMC-L4-GLOB-v2.0); [DOI 10.5067/GHCMC-4FM02](https://doi.org/10.5067/GHCMC-4FM02) |
| `cmc_v3` | Canadian Meteorological Centre, GHRSST CMC 0.1° global foundation SST, version 3.0 | [Product record](https://podaac.jpl.nasa.gov/dataset/CMC0.1deg-CMC-L4-GLOB-v3.0); [DOI 10.5067/GHCMC-4FM03](https://doi.org/10.5067/GHCMC-4FM03) |
| `gamssa` | Australian Bureau of Meteorology, GHRSST GAMSSA daily global 0.25° foundation SST, version 1.0 | [Product record](https://podaac.jpl.nasa.gov/dataset/GAMSSA_28km-ABOM-L4-GLOB-v01); [DOI 10.5067/GHGAM-4FA1A](https://doi.org/10.5067/GHGAM-4FA1A) |
| `gpb_5km` | NOAA/OSPO, GHRSST global **nighttime** foundation SST, version 1.0 | [Product record](https://podaac.jpl.nasa.gov/dataset/Geo_Polar_Blended_Night-OSPO-L4-GLOB-v1.0); [DOI 10.5067/GHGPN-4FO02](https://doi.org/10.5067/GHGPN-4FO02) |
| `oisst` | NOAA/NCEI, daily 0.25° Optimum Interpolation SST, version 2.1 | [Product and recommended citations](https://www.ncei.noaa.gov/products/optimum-interpolation-sst); Huang et al., improvements to DOISST v2.1, [article DOI 10.1175/JCLI-D-20-0166.1](https://doi.org/10.1175/JCLI-D-20-0166.1) |
| `ostia` | UK Met Office, GHRSST operational global foundation SST, GDS version 2 | [Product record](https://podaac.jpl.nasa.gov/dataset/OSTIA-UKMO-L4-GLOB-v2.0); [DOI 10.5067/GHOST-4FK02](https://doi.org/10.5067/GHOST-4FK02) |

The OSTIA entry is the operational product, not the separately catalogued
reprocessed OSTIA product. OISST's linked article is a scientific reference,
not an END dataset DOI. END has not assigned a DOI to its conversion.

## Data terms and retained notices

CMC V2, CMC V3, GAMSSA and GPB05 source files inspected for this inventory carry
the GHRSST free/open data-use notice. Retain their product identities, producer
attribution and notices. Follow the [PO.DAAC data-use and citation
guidance](https://podaac.jpl.nasa.gov/CitingPODAAC) alongside the linked product
record; archive availability alone is not a new license granted by END.

For NOAA OISST, use the [NCEI open data
policy](https://www.ncei.noaa.gov/sites/default/files/2023-12/NCEI%20PD-10-2-02%20-%20Open%20Data%20Policy%20Signed.pdf)
and the product citation above. NCEI distinguishes federally produced data from
third-party archive material. END does not apply that policy indiscriminately
to the other producers' collections.

Latest inspected OSTIA input identifies the Copernicus Marine Service SLA;
older retained metadata identifies GMES data policy. Follow the applicable
Copernicus Marine license and [citation and acknowledgement
guidance](https://help.marine.copernicus.eu/en/articles/4444611-citing-copernicus-marine-products-and-services).
That guidance distinguishes redistribution from derivative products. END must
record the applicable historical terms and redistribution acknowledgement in
the release manifest before distributing the mixed historical OSTIA archive.
This remains a release gate; documentation publication does not grant rights
to unpublished data.

## Citing an END conversion

Cite the upstream product first. Then identify END Sea Surface Temperature
Collections, collection name, public release/snapshot ID, group, access date,
and the dates and spatial region used. State that END converted the source
arrays into Icechunk-backed Zarr V3. For results made with this repository,
also record its commit and dependency versions.

Keep preliminary/final revision information and report missing dates or fields.
The [dataset guide](README.md) explains duplicate-date selection, OSTIA group
overlap and the current quality limitations. No blanket data license is asserted
for all six collections; each public release must retain its source terms.
