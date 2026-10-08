# geofeeds

[![Catalog](https://github.com/opengeoip/geofeeds/actions/workflows/catalog.yml/badge.svg)](https://github.com/opengeoip/geofeeds/actions/workflows/catalog.yml)
[![Latest](https://img.shields.io/github/v/release/opengeoip/geofeeds?label=catalog)](https://github.com/opengeoip/geofeeds/releases/latest)

The list of IP geolocation feeds ([RFC 8805](https://www.rfc-editor.org/rfc/rfc8805)) that [geoip-builder](https://github.com/opengeoip/geoip-builder) uses.

Every day, the catalog is rebuilt from the latest registry dumps of RIPE NCC, APNIC, AFRINIC and LACNIC and from ARIN's geofeed references, then merged with [`manual.csv`](manual.csv). When it changes, a new release is published with `geofeeds.csv`:

```
https://github.com/opengeoip/geofeeds/releases/latest/download/geofeeds.csv
```

## Columns

| Column | Content |
|---|---|
| `url` | the geofeed |
| `network` | the prefix of the registry object referencing it ([RFC 9632](https://www.rfc-editor.org/rfc/rfc9632)), empty for a geofeed no registry references |
| `source` | `afrinic`, `apnic`, `arin`, `lacnic`, `ripencc`, or `manual` |
| `asn` | for a geofeed no registry references, the ASes of its publisher, separated by spaces |

## Adding a geofeed

Geofeeds referenced from a registry object are found automatically. For one that is not, open a pull request adding a line to `manual.csv`:

```
https://example.net/geofeed.csv,,manual,64500 64501
```

Its entries are only trusted for prefixes announced in BGP by the declared ASes. List only ASes whose registry records name the publisher of the feed. A line with a prefix in the `network` column anchors the feed on that prefix instead.

## License

GPL-3.0-or-later, see [LICENSE](LICENSE). The catalog is derived from registry data with its own terms of use.
