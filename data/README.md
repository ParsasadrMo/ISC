[README.md](https://github.com/user-attachments/files/35037426/README.md)
# ISC case-study dataset

`H3Polygon4ISC.gpkg` contains the spatial predictors and labels used to evaluate the Integrated Spatial–Classification (ISC) framework for Mississippi Valley-type (MVT) Zn–Pb prospectivity mapping in Canada.

## Download

Download `H3Polygon4ISC.gpkg` from the **Assets** section of the repository's [v1.0.0 release] (https://github.com/ParsasadrMo/ISC/releases/tag/v1.0.0)(../../releases/tag/v1.0.0).

The dataset is distributed as a release attachment. Its file size is approximately 849 MiB (889,962,496 bytes).

## File placement

Place `H3Polygon4ISC.gpkg` in the repository's main directory, beside `ISC_Implementation.ipynb`. Launch JupyterLab from that directory so the notebook can resolve its input and output paths.

This `data/` directory contains the dataset documentation. The current notebook loads the GeoPackage from its working directory using

```python
cube = gpd.read_file(
    "H3Polygon4ISC.gpkg",
    engine="pyogrio",
    use_arrow=True,
)
```

## Spatial representation

| Property | Description |
| --- | --- |
| File format | GeoPackage (`.gpkg`) |
| Geometry | Polygon |
| Spatial units | 1,820,346 H3 cells |
| H3 resolution | 7 |
| Study region | Canadian study grid |
| Geometry CRS | EPSG:3978 — NAD83 / Canada Atlas Lambert |
| Predictors | 22 fields, `F_1`–`F_22` |

## Field definitions

| Field | Description |
| --- | --- |
| `H3id` | H3 cell identifier |
| `F_1` | First vertical derivative of gravity data |
| `F_2` | Bouguer gravity |
| `F_3` | Horizontal gradient magnitude of gravity data |
| `F_4`–`F_9` | Gravity-worm proximity predictors at 5, 10, 15, 20, 25, and 30 km, respectively |
| `F_10` | First vertical derivative of magnetic data |
| `F_11` | Horizontal gradient magnitude of aeromagnetic data |
| `F_12` | Reduced-to-pole aeromagnetic data |
| `F_13` | Tilt derivative of magnetic data |
| `F_14` | Minimum geological age predictor |
| `F_15` | Maximum geological age predictor |
| `F_16`–`F_21` | Magnetic-worm proximity predictors at 5, 10, 15, 20, 25, and 30 km, respectively |
| `F_22` | Binary predictor representing sedimentary bedrock geological polygons |
| `longitude` | Longitude in decimal degrees |
| `latitude` | Latitude in decimal degrees |
| `target` | Positive-label indicator. A value of `1` identifies a cell hosting known MVT Zn–Pb mineralization |
| `SetA` | Negative-label membership indicator for Set A |
| `SetB` | Negative-label membership indicator for Set B |
| `GProvince` | Geological province attribute |
| `geometry` | H3 cell polygon geometry |

The proximity distances identify the predictor layers. Predictor values reflect the preprocessing used for modelling. Detailed source attribution, transformations, and missing-data treatment are described in the associated manuscript and Parsa et al. (2026).

**Reference to complete before publication:** [Insert the full citation for Parsa et al. (2026).]

## Label definitions

**Positive labels.** Cells with `target = 1` host known MVT Zn–Pb mineralization.

**Set A.** Cells with `SetA = 1` belong to the negative-label set randomly selected from locations at least 100 km from known MVT Zn–Pb mineralization.

**Set B.** Cells with `SetB = 1` belong to the negative-label set randomly selected from locations at least 100 km from known MVT Zn–Pb mineralization.

A value of `0` in a label column indicates absence of that label assignment. Cells with `target = 0` may include unlabelled cells. The negative-label sets represent the background classes adopted for this experiment.

The modelling workflow evaluates Set A and Set B independently. Cells carrying both positive and negative labels are treated as positive and excluded from the corresponding negative set during modelling.

## Use in evaluation

Supervised training uses positive cells and cells in the selected negative-label set. The full study grid, including unlabelled cells, is retained for prospectivity prediction and exploration-coverage calculations.

Exploration coverage is calculated as the number of selected cells divided by the total number of study cells. ROC evaluation uses held-out positive and negative cells, while SR evaluation relates the recovery of held-out positive cells to full-grid coverage. ISC combines this coverage with the held-out false-positive rate.

## Citation and reuse

Consult the repository's main README for the associated manuscript and citation details.

## Data source and reuse terms

This dataset is derived from:

Parsa, M., Lawley, C.J.M., Schetselaar, E., Martins, T., and
Thompson, A., 2026. Multicomponent geospatial data for predictive
mapping of Canadian critical minerals. Geological Survey of
Canada, Open File 9270e.
https://doi.org/10.4095/p80q4bhma6

The accompanying source publication permits personal and public
non-commercial reproduction with attribution. Commercial reproduction
and distribution require written permission from Natural Resources
Canada.

H3Polygon4ISC.gpkg is a modified derivative prepared for the ISC
case study. Modifications include predictor selection, an additional
sedimentary-bedrock predictor, revised labels, and polygon geometry.

This derivative has been prepared by the study authors. Its distribution
does not imply endorsement by Natural Resources Canada.

Source permissions contact:
copyright-droitdauteur@nrcan-rncan.gc.ca
