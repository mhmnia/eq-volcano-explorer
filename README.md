# Earthquake–Volcano Proximity Explorer

A single-page tool that answers one question quickly: **after a large earthquake, which volcanoes are close enough to be worth a look?**

Load the USGS earthquake catalogue for a time window and magnitude threshold, click any event, and the tool lists every Smithsonian GVP Holocene volcano inside your chosen radius — with distance, azimuth, last known eruption and GVP activity evidence — on a schematic proximity plot and an optional satellite basemap.

**Live version → https://mhmnia.github.io/eq-volcano-explorer/**

---

## What it does

- Queries the **USGS FDSN event service** live, for any date range and minimum magnitude.
- Plots the catalogue as a magnitude–time bubble chart; click a bubble to select an event.
- Computes great-circle distance and azimuth from the epicentre to every volcano in the catalogue, and filters to a radius of 100, 250, 500 or 1,000 km.
- Colours volcanoes by how recently they erupted, from the GVP *Last Known Eruption* field.
- Draws the result twice: as a schematic azimuth–distance plot, and on a pannable Esri or OpenStreetMap basemap.
- Clicking a volcano on the map highlights its row in the table, and the reverse.

## Volcano catalogue

The **Smithsonian GVP Holocene volcano list** ships with the tool in `data/` and loads automatically — nothing to upload before you start. It contains 1,214 volcanoes (VOTW v5.4.0, downloaded 16 August 2026), converted to UTF-8.

To use a newer or different catalogue, open *Use a different catalogue file* in step 2 and pick a CSV, TSV or GeoJSON file. Column names are matched flexibly, so most GVP exports work without editing. **The file is read in your browser and is never uploaded anywhere.**

To update the bundled list, download the [Holocene Volcano List](https://volcano.si.edu/volcanolist_holocene.cfm) as an XML Excel file, save it as CSV, and replace `data/gvp_holocene_volcanoes.csv`.

## Running it locally

The page reads its own data file, so it needs to be served over HTTP rather than opened by double-clicking:

```bash
git clone https://github.com/mhmnia/eq-volcano-explorer.git
cd eq-volcano-explorer
python -m http.server
# open http://localhost:8000
```

No build step, no dependencies. One HTML file plus one CSV.

## An important caveat

Proximity is **spatial context only**. A volcano inside the search radius does not by itself establish that an earthquake triggered activity there. Static distance says nothing about static or dynamic stress change, the state of the magmatic system, or the timing of any response. Treat the output as a screening list, not a result.

The colour scheme reflects the GVP *Last Known Eruption* field, which is a static compilation — it cannot tell you what is erupting today. For that, use the [GVP Weekly Activity Report](https://volcano.si.edu/reports_weekly.cfm).

## Data sources

- Earthquakes: [USGS FDSN event web service](https://earthquake.usgs.gov/fdsnws/event/1/)
- Volcanoes: Global Volcanism Program, 2026. *Volcanoes of the World* (v. 5.4.0). Smithsonian Institution, compiled by E. Venzke. https://doi.org/10.5479/si.GVP.VOTW5-2026.5.4
- Basemap tiles: Esri World Imagery, with OpenStreetMap as fallback

## Citing

If this tool contributed to your work, please cite it — see `CITATION.cff`, or:

> Mohammadnia, M. (2026). *Earthquake–Volcano Proximity Explorer* (v1.0.0). Zenodo.

## Licence

GPL-3.0-only. See `LICENSE`.

## Author

**Mohammadhossein Mohammadnia**, PhD — solid-Earth geodesy, InSAR, volcano deformation
[mhmnia.github.io](https://mhmnia.github.io/) · [ORCID 0009-0000-2193-2980](https://orcid.org/0009-0000-2193-2980) · mh.mohammadnia1@gmail.com
