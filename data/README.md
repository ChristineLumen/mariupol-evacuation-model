# data/ — optional evidence layers

## unosat_mariupol.geojson (recommended)
UNOSAT building-damage assessments for Mariupol (code CE20220223UKR): download the geodata
from https://data.humdata.org (search "UNOSAT Mariupol"), convert shapefile → GeoJSON if
needed (QGIS or `ogr2ogr -f GeoJSON unosat_mariupol.geojson input.shp`), and save here.
The viewer detects damage class from any property matching /dmg|damage|class|grad/i
(destroyed / severe / moderate / possible, or 4/3/2/1) and filters by any date-like property.
Points render as dots; polygons (e.g. after a QGIS spatial join to building footprints)
render as filled footprints; lines render as damaged road segments.

## osm_buildings.json (optional, for offline/instant Buildings mode)
```bash
curl -X POST https://overpass-api.de/api/interpreter \
  --data-urlencode 'data=[out:json][timeout:60];way["building"](47.05,37.45,47.17,37.72);out geom;' \
  -o osm_buildings.json
```
Building footprints © OpenStreetMap contributors (ODbL).

Layer priority in the tool: real UNOSAT geodata → OSM footprints coloured by district
chronology (labelled illustrative) → district-level zone illustration.
