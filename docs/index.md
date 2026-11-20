[index.md](https://github.com/user-attachments/files/35039061/index.md)
---
layout: default
title: Integrated Spatial–Classification Evaluation
---

# Integrated Spatial–Classification (ISC) Evaluation

## Mineral prospectivity mapping

ISC evaluates mineral prospectivity models by combining exploration coverage and false-positive rate while retaining true-positive rate on the vertical axis. Its weighting parameter, α, allows model comparisons to reflect different priorities for spatial selectivity and classification performance.

This project demonstrates the framework using continental-scale mapping of Mississippi Valley-type (MVT) Zn–Pb mineralization in Canada and two alternative negative-label sets.



## Dataset

The input file, `H3Polygon4ISC.gpkg`, contains 1,820,346 H3 resolution-7 polygon cells, 22 predictors, known MVT Zn–Pb mineralization labels, and two negative-label sets. Polygon geometry is stored in EPSG:3978.

Set A is derived from selected magmatic mineralization. Set B comprises randomly selected locations at least 100 km from known MVT Zn–Pb mineralization.



## Run the workflow

1. Download the repository using **Code → Download ZIP** on GitHub and extract it.
2. Download `H3Polygon4ISC.gpkg` from the release assets and place it beside `ISC_Implementation.ipynb`.
3. Install the dependencies in a Python environment using the command below.
4. Launch JupyterLab from that directory and run the notebook cells in order.

```bash
python -m pip install -r requirements.txt
python -m jupyterlab
```

The notebook covers data visualization, balanced Random Forest ensembles, five-fold cross-validation, evaluation curves, and final prospectivity mapping. Evaluation uses 50 equally spaced α values from 0 to 2.5. Exploration coverage is measured over the full study grid using cell counts.



## Manuscript and authors

The associated manuscript is under review. Its publication details will be added when available.

Mohammad Parsa · Steven E. Zhang · Renato Cumani

## Data source and reuse

The case-study dataset is derived from *Multicomponent geospatial data for predictive mapping of Canadian critical minerals*, Geological Survey of Canada, Open File 9270e, with modifications for this study.

[Source publication](https://doi.org/10.4095/p80q4bhma6)
