# END open data examples

Documentation and reproducible examples for END's public data work.

## Sea surface temperature

[END Sea Surface Temperature Collections](endcorp-sst/README.md) documents six
global SST analyses converted to Zarr V3 and versioned with Icechunk.

**Status: public data release pending.** Documentation is available now. The
tutorial needs the endpoint and snapshot from the first validated public release;
it is not yet an anonymously runnable dataset download. No active AWS sponsorship
or Registry listing is claimed.

- [Dataset guide and data dictionary](endcorp-sst/README.md)
- [Measured coverage and quality inventory](endcorp-sst/coverage.json)
- [Get To Know A Dataset notebook](endcorp-sst/get-to-know-a-dataset.ipynb)
- [Source rights and citation guide](endcorp-sst/source-rights.md)
- [Support and contributions](CONTRIBUTING.md)

## Run the tutorial after public release

Use Python 3.12 in a virtual environment:

```sh
python -m venv .venv
source .venv/bin/activate
python -m pip install -r endcorp-sst/requirements.txt
jupyter lab endcorp-sst/get-to-know-a-dataset.ipynb
```

Set the notebook's bucket and immutable snapshot from the validated public
manifest when it is published. The example defaults to anonymous reads and
does not silently fall back to AWS credentials. It selects seven days in a
small equatorial Pacific region, plots SST and computes a regional anomaly.

## License

END-authored documentation and example code are [MIT licensed](LICENSE).
Upstream data and retained source metadata are excluded from that license;
their product-specific terms and attribution remain applicable.
