# Humanitarian Corridors Under Siege: Mariupol 2022
## Live Website: https://christinelumen.github.io/mariupol-evacuation-model/
## Standalone severity model: https://christinelumen.github.io/mariupol-evacuation-model/severity-standalone.html
**Retrospective decision-support prototype for civilian evacuation under IHL · not operational guidance**

A two-axis evacuation decision matrix combining **Severity** (daily danger from hostilities, deprivation, and infrastructure destruction) and **Feasibility** (satellite-verified building damage, UNOSAT official assessments, and nighttime light loss across evacuation windows) for the siege of Mariupol, 5 March – 20 May 2022.

**Research question.** *How can and should AI tools be used to enhance the protection and evacuation of civilians during armed conflict, and how do they support or challenge obligations under International Humanitarian Law?*

**Central finding.** Modelled severity crosses critical thresholds in mid-March 2022; the negotiated evacuation mechanism envisaged by GC IV art. 17 arrived on 30 April — roughly eight weeks after the modelled peak. The binding constraint was not information but consent.

## Quick start

**Live:** https://christinelumen.github.io/mariupol-evacuation-model/

**Local:** serve the folder (required for JSON data and iframe loading):

```bash
python3 -m http.server
# open http://localhost:8000/
```

Internet is required for base map layers (Leaflet CDN, Esri Wayback Archive imagery, NASA GIBS, OSM).

## What it does

### Axis 1 — Severity

Select any date of the siege and the tool renders: the corridor regime in effect and its route on a schematic front-line map; the observed variables for that date; a six-component severity score with a five-phase classification; and a generated written assessment with legal anchors.

Severity `S` is a generalised power mean (p = 6, weakest-link) of six normalised components — hostility intensity, kinetic proximity, protection risk, cold burden, deprivation clock, infrastructure damage — multiplied by a vulnerability weight (Vw = 1.114). Full definitions: **[docs/METHODOLOGY.md](docs/METHODOLOGY.md)**.

### Axis 2 — Feasibility

Four evacuation windows with:
- **Satellite imagery comparison** — before/after Esri Wayback Archive imagery with opacity slider
- **UNOSAT official damage assessment** — 783 structures (14 Mar 2022) and 5,647 structures (7–12 May 2022) from UNOSAT code CE20220223UKR, overlaid as colour-coded damage markers
- **Nighttime light simulation** — 45,544 building centroids from OSM with deterministic light-survival modelling calibrated to NASA VIIRS Black Marble measurements, visualising infrastructure collapse across siege phases

### Assessment conclusion

A dynamically generated conclusion synthesising severity findings, corridor regime, dominant risk drivers, IHL obligations, and the factual predicate for evacuation — updates with each selected date.

## Repository structure

```
index.html                  combined two-axis decision matrix (main page)
severity.html               Axis 1 — severity model (iframe source)
teresa.html                 Axis 2 — feasibility analysis (iframe source)
severity-standalone.html    original standalone severity page
unosat_mariupol_damage.json UNOSAT damage points (March + May 2022)
mariupol_lights.json        45K building centroids for nighttime light simulation
docs/METHODOLOGY.md         model definitions, formulas, data tables, references
data/                       optional evidence layers (see data/README.md)
imagery/                    optional dated satellite crops (see imagery/README.md)
CITATION.cff                citation metadata
```

## Data sources

| Source | Usage |
|---|---|
| [ACLED](https://acleddata.com) | Armed conflict events, Mariupol raion, Mar–May 2022 |
| [UNOSAT/UNITAR](https://unosat.org) | Satellite-detected building damage (CE20220223UKR) |
| [NASA VIIRS Black Marble](https://blackmarble.gsfc.nasa.gov) | Nighttime light intensity, calibrated against pre-invasion baseline |
| [Planet Labs](https://www.planet.com) | High-cadence satellite imagery for change detection |
| [Esri Wayback Archive](https://livingatlas.arcgis.com/wayback/) | Historical satellite imagery tiles |
| [ERA5 / ECMWF](https://cds.climate.copernicus.eu) | Temperature reanalysis |
| [WorldPop](https://www.worldpop.org) | Gridded population estimates |
| [OpenStreetMap](https://www.openstreetmap.org) | Building footprints (45,544 structures via Overpass API) |

## Honest limits

Retrospective and not validated against observed departure flows; event reporting degrades inside a besieged city precisely when severity peaks; normalisation bounds, the p = 6 exponent, and phase thresholds are documented conventions pending re-estimation; the same data fusion that prioritises evacuation could support targeting — movement data is protection-sensitive. Full list in the methodology.

## Citation

See `CITATION.cff`. Front line, controlled areas, and district damage zones are approximate; parties'-conduct summaries are descriptive and attributed (OCHA/ICRC/OHCHR), not adjudicative.
