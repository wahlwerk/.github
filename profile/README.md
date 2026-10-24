# wahlwerk

**Electoral and parliamentary systems as rules-as-code.** A deterministic Python engine that
replays real election results under any version of an electoral law, so that a reform can
be tested seat by seat against history.

The engine knows no country: apportionment methods, thresholds and Ausgleich are general
building blocks, and a system is a composition of them. The first systems implemented are
German Landtage.

An electoral law is written as a *protocol*: an ordered tuple of small, frozen steps, each
citing the section it implements (`Sec. 35 (8) LWG LSA`). Applying it to the votes of an
election returns the chamber. A counterfactual is the same votes under a different
protocol: change one step, replay, compare.

## Reproduced exactly

Every implemented law is held to the official result, party by party, Wahlkreis and list
seats alike, in a golden test.

| Landtag | Law | Seats |
| --- | --- | --- |
| Sachsen-Anhalt 2021 | LWG LSA | 97 (83 raised for Mehrsitze) |
| Sachsen-Anhalt 2026 | LWG LSA | 83 |
| Mecklenburg-Vorpommern 2011 | LKWG M-V | 71 |
| Mecklenburg-Vorpommern 2016 | LKWG M-V | 71 |
| Mecklenburg-Vorpommern 2021 | LKWG M-V | 79 (Überhang and Ausgleich) |

## Repositories

`wahlwerk` is the package; the other repositories feed it data, use it or show its results.

| Repo | What it holds |
| --- | --- |
| [**wahlwerk**](https://github.com/wahlwerk/wahlwerk) | **the package and engine**: laws as protocols, pydantic models, exact arithmetic (`Fraction`, never `float`), ties as results |
| [wahlwerk-data](https://github.com/wahlwerk/wahlwerk-data) | election data for the engine: normalised bundles and party registries, each with source, licence and SHA-256 |
| [wahlwerk-ui](https://github.com/wahlwerk/wahlwerk-ui) | seat charts for the engine: dependency-free SVG, the optional extra `wahlwerk[ui]` |
| [wahlwerk-site](https://github.com/wahlwerk/wahlwerk-site) | the website: each component of the engine explained with elections it reproduces |

## Principles

- **Golden tests are the product.** A law counts as implemented when it reproduces the
  official Sitzverteilung exactly.
- **Exact arithmetic.** Float rounding hides real ties and manufactures fake ones.
- **Ties are a result.** Where the law prescribes a Losentscheid, the engine returns a `Tie`
  instead of letting sort order decide.
- **Sources travel with the data.** Every bundle carries its publisher, licence and the
  attribution the publisher requires.

Not in scope: forecasting, voter-behaviour models, simulating the Bundesverfassungsgericht.

## Licence

Code is GPL-3.0. Election data keeps the licence of its source (usually
[dl-de/by-2-0](https://www.govdata.de/dl-de/by-2-0)), recorded in each bundle.
