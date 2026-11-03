# Fit Extension for UCP

**`ai.vsize.shopping.fit`** · Draft 1 · November 2026

A vendor-namespace extension to the [Universal Commerce Protocol](https://github.com/Universal-Commerce-Protocol/ucp)
that makes footwear fit a **measurable property** of a catalog variant.

> Fit is a comparison between two measurements, not a summary of reviews.

An agent buying shoes on someone's behalf cannot try the shoe on. Today UCP carries size as a
label (`Size: EU 40`) and fit as free text through `ask`. Neither is something an agent can
compute with. This extension adds three things:

1. **The variant carries its internal dimensions**, in millimetres, with a tolerance and a source.
2. **The buyer may supply a consented foot profile** in request context, one entry per foot.
3. **When both are present, the variant carries a zone-by-zone fit assessment** with an explicit
   confidence. `unknown` is a valid verdict.

Field names follow the existing vocabulary: ISO 19409 and ISO 19410-1 for the inside of the shoe,
ISO 7250 and Mondopoint (ISO 9407) for the foot.

## Where things live

| What | Here | Authoritative URL |
|---|---|---|
| Schema | [`schemas/fit.json`](schemas/fit.json) | https://vsize.ai/ucp/schemas/fit.json |
| Specification | [`spec/index.html`](spec/index.html) | https://vsize.ai/ucp/fit |
| Examples | [`examples/`](examples/) | |
| Discussion | | https://github.com/Universal-Commerce-Protocol/ucp/discussions/1027 |
| Background | | https://vsize.ai/insights-fit-extension.html |

UCP binds a namespace to the domain that serves its schema, so the copy at `vsize.ai` is the one
agents resolve. This repository is the source, the place to read it with history, and the place to
open issues or pull requests.

## Extends

- `dev.ucp.shopping.catalog.search`
- `dev.ucp.shopping.catalog.lookup`

## Non-goals

- No reviews, keep rates or return statistics.
- No size-system conversion (ISO 19407 covers that).
- No storage of foot data on the business side.
- Footwear only in this draft.

## Open questions

1. Do `internal_dimensions` belong on the catalog variant, or in a separate capability?
2. May `foot_profile` travel in catalog `context`, or does buyer measurement data need its own
   consent path, like identity linking?
3. May `vocabulary` reference an externally governed, paid standard such as ISO 19409?

## Path

Published under a vendor namespace, as the UCP contribution guide recommends for emerging use
cases. If a second party, a merchant or a scanning provider, wants to expose or consume these
fields, the intent is to propose `dev.ucp.shopping.fit` through an Enhancement Proposal to the
Shopping Tech Council.

## Contributing

Open an issue for questions or proposed changes to the schema. Pull requests welcome. Keep the
principles: millimetres, tolerance and source on every dimension, confidence on every assessment,
no opinions dressed as measurements.

## License

Apache 2.0, in line with UCP. Published by VSIZE, Novainvent AB, Halmstad, Sweden.
