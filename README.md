# Fastener Standards Data

Open dimensional data for common metric and imperial fastener standards.

**872 records · 16 standards · CC BY 4.0.**

Maintained by [Longze Engineering](https://lz-engineering.com) (Hebei Longze Metal Products Manufacturing Co., Ltd.),
a fastener manufacturer. We publish the dimensional data behind our size charts so that engineers,
tooling engineers and software can use it without scraping pages.

## Files

| File | Size | Description |
|---|---|---|
| fastener-standards.csv | ~94 KB | Flat table, one row per standard + size + grade + finish |
| fastener-standards.json | ~373 KB | Same data, JSON array |
| MANIFEST.json | - | Record count, file hashes, build metadata |
| LICENSE | - | CC BY 4.0 legal code |

## Standards covered

| Standard | System | Component | Records |
|---|---|---|---|
| DIN 931 | Metric | bolt | 119 |
| DIN 933 | Metric | bolt | 154 |
| ISO 4014 | Metric | bolt | 119 |
| ISO 4017 | Metric | bolt | 154 |
| DIN 934 | Metric | nut | 44 |
| ISO 4032 | Metric | nut | 44 |
| DIN 125-A | Metric | washer | 30 |
| ISO 7089 | Metric | washer | 30 |
| DIN 127-A | Metric | spring washer | 54 |
| DIN 7980 | Metric | spring washer | 32 |
| ASME B18.2.1 | Imperial | bolt | 22 |
| ASME B18.2.2 | Imperial | nut | 22 |
| ASME B18.3 | Imperial | screw | 18 |
| ASME B18.21.1 | Imperial | spring washer | 18 |
| DIN 912 | Metric | screw | 6 |
| ISO 4762 | Metric | screw | 6 |

## Field definitions

Numbers are nominal dimensions in millimetres. A value is null when the field does not apply
to that component, or when the upstream table did not publish it (see Known limitations).

| Field | Type | Unit | Applies to | Notes |
|---|---|---|---|---|
| standard | string | - | all | e.g. DIN 931 |
| size | string | - | all | Metric M6 or imperial 1/4, 1-1/8 |
| system | string | - | all | Metric or Imperial |
| grade | string | - | all | Property class (8.8) or material grade (A4-70); as catalogued |
| finish | string | - | all | Plain, Stainless Steel, Zinc Clear; as catalogued |
| component | string | - | all | bolt, nut, screw, spring washer, washer |
| width_across_flats_mm | number or null | mm | bolt, nut; screw (socket key) | Width across flats. For DIN 912 / ISO 4762 socket head screws this is the hex socket width across flats (key size); ASME B18.3 null because the reference table gives head diameter, not a WAF |
| head_height_mm | number or null | mm | bolt, nut, screw (null for ASME B18.2.1 / B18.2.2) | Head height k for bolts/screws; nut height m for nuts |
| inner_dia_mm | number or null | mm | washer, spring washer | Washer bore (d1) |
| outer_dia_mm | number or null | mm | washer, spring washer | Washer outside diameter (d2) |
| thickness_mm | number or null | mm | washer, spring washer | Washer thickness (h for flat washers, s for spring washers) |
| tensile_mpa | number or null | MPa | bolt, screw | Tensile strength of the property class / material grade |
| yield_mpa | number or null | MPa | bolt, screw | Yield strength (or 0.2 percent proof stress) of the class |
| weight_per_1000_kg | number or null | kg / 1000 pcs | DIN 7980 only | Nominal mass, reference material |
| source | string | - | all | Public reference table the record was catalogued from |

## Null means "not applicable", not zero

- inner_dia_mm null on a bolt means the part has no bore - not a 0 mm bore.
- width_across_flats_mm null on a washer means it has no hex; null on ASME B18.3 means the
  reference table publishes head diameter instead of a width across flats.
- tensile_mpa null on nuts and washers means the value is not a property of that component's
  standard (nut property classes define proof load stress, washer standards define none).

## Known limitations

1. **Nominal values only.** Each standard defines its own tolerances; those tolerances are not
   included here. Our size charts (see Related) show the tolerance ranges per product grade.
2. **This is a convenience dataset, not a normative document.** For design, certification or
   acceptance testing, use the standard text itself.
3. **Thread pitch is not included in v1.0.0.** Pitch is in the standards and on our size charts,
   but it is not part of this release.
4. **Nuts:** mechanical properties are null because nut property classes specify proof load
   stress, not a tensile strength.
5. **Washers:** mechanical properties are null; washer standards do not define them.
6. **Socket head cap screws:** DIN 912 / ISO 4762 publish the hex socket width across flats as
   width_across_flats_mm. ASME B18.3 head diameter and socket size are not included in v1.0.0.
7. **DIN 125-A / ISO 7089** list preferred sizes only. Non-preferred sizes M26, M28, M32 and
   M35 were dropped from v1.0.0 because the upstream reference rows carried the next size's
   dimensions (label offset) and could not be verified.
8. **ASME B18.2.1 / B18.2.2:** only width across flats is published. The head height
   (ASME B18.2.1) and nut height (ASME B18.2.2) columns of the upstream reference table do not
   match the published ASME values, so they are null in v1.0.0 rather than wrong.
9. **ASME B18.21.1** rows are helical spring lock washers; the standard also covers other
   washer types, so component is spring washer and grade/finish are as catalogued.
10. **Weight** is published only where the upstream table gives a mass (DIN 7980 in v1.0.0).
11. **ISO 4014** nominal dimensions are identical to ISO 4017 (same bolt, part-threaded vs
    fully-threaded); the nominal-value table is shared.
12. **One finish per grade.** The dataset keeps one representative finish per
    (standard, size, grade): stainless grades use Stainless Steel, carbon classes use Plain.
    DIN 912 / ISO 4762 keep Zinc Clear for every grade in v1.0.0 because that is the first
    listing in the upstream catalogue, including for the stainless grades listed there.
13. Grade/finish combinations are as catalogued in our production database and may be broader
    than one manufacturer's current stock.

## How this was built

Nominal values come from DIN, ISO and ASME standard dimension tables; ASME width-across-flats
values were additionally checked against the published ASME dimension tables. Spring washer
dimensions (DIN 127-A, DIN 7980) come from a manufacturer manual cross-checked against two
independent public sources. Records were compiled from public reference tables (see the source
column) and cross-checked against our published size charts. Where sources disagreed we did not
average - the nominal standard value was used.

## License

Data: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) - use it freely, including
commercially, with attribution.

Attribution example:

> Fastener standards data from Longze Engineering (https://lz-engineering.com)

The full license text is in LICENSE.

## Citation

If you use this dataset, please cite:

> Longze Engineering (2026). Fastener Standards Data (Version 1.0.0) [Data set].
> Hebei Longze Metal Products Manufacturing Co., Ltd. https://github.com/w1372068887-pixel/longze-fastener-data

An archived version with a DOI will be deposited with Zenodo and listed here.

## Related

- Dataset repository: https://github.com/w1372068887-pixel/longze-fastener-data
- Open data landing page: https://lz-engineering.com/open-data/
- Interactive size charts: https://lz-engineering.com/library/
- Mechanical property reference: https://lz-engineering.com/mechanical-properties/
