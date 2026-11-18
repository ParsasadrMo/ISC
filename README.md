# Integrated Spatial–Classification (ISC) Evaluation for Mineral Prospectivity Modelling

Implementation of the ISC framework, demonstrated through continental-scale prospectivity mapping for Mississippi Valley-type (MVT) Zn–Pb mineralization in Canada.

ISC evaluates the recovery of known mineralized cells against a weighted combination of exploration coverage and false-positive rate. The workflow compares models trained using two alternative negative-label sets and evaluates their spatial selectivity and classification performance using success-rate (SR), receiver operating characteristic (ROC), and ISC curves.

## Associated manuscript

**Title:** A Unified Evaluation Framework for Data-Driven Mineral Prospectivity Modelling

**Authors:** Mohammad Parsa, Steven E. Zhang, and Renato Cumani

**Status:** Under review. Publication details and the article DOI will be added when available.

## Contents

| File | Description |
| --- | --- |
| `ISC_Implementation.ipynb` | Data loading, covariate visualization, label mapping, modelling, cross-validation, evaluation, and prospectivity mapping |
| `requirements.txt` | Python dependencies; to be added |
| `H3Polygon4ISC.gpkg` | Input dataset, downloaded separately and placed beside the notebook |
| `ModelingResults/` | Modelling outputs generated when the notebook runs |

## Dataset

The input dataset, `H3Polygon4ISC.gpkg`, is a polygon GeoPackage containing 1,820,346 H3 cells across the Canadian study region. The grid uses H3 resolution 7, and the polygon geometry is stored in EPSG:3978.

**Download:** [Data download link to be added]

Place the downloaded GeoPackage in the same directory as `ISC_Implementation.ipynb`. The current notebook reads the filename directly from its working directory.

| Field | Description |
| --- | --- |
| `H3id` | H3 cell identifier |
| `F_1`–`F_21` | Geophysical and geochronological predictors |
| `F_22` | Binary predictor representing sedimentary bedrock geological polygons |
| `longitude`, `latitude` | Geographic coordinates used for visualization and H3 indexing |
| `target` | Positive-label indicator, with `1` identifying a cell hosting known MVT Zn–Pb mineralization |
| `SetA` | Negative-label indicator for Set A, derived from selected magmatic mineralization |
| `SetB` | Negative-label indicator for Set B, derived from randomly selected locations at least 100 km from known MVT Zn–Pb mineralization |
| `GProvince` | Geological province attribute |
| `geometry` | H3 cell polygon geometry |

A value of `1` in `SetA` or `SetB` identifies membership in that negative-label set. Cells outside the selected positive and negative classes remain available for full-grid prediction and exploration-coverage calculations.

Missing-data treatment follows the procedure described by Parsa et al. (2026). The complete reference and detailed predictor descriptions will be added before release.

## Installation

The uploaded notebook records Python 3.10.20 in its metadata. Its dependencies include NumPy, pandas, GeoPandas, Pyogrio, PyArrow, Matplotlib, Cartopy, scikit-learn, H3, and Pillow. JupyterLab is required to run the notebook interactively.

Once `requirements.txt` has been added, install the dependencies in a dedicated environment using

```bash
python -m venv .venv
```

Activate the environment on Windows using

```powershell
.venv\Scripts\Activate.ps1
```

Or on macOS and Linux using

```bash
source .venv/bin/activate
```

Then install the dependencies and launch JupyterLab from the directory containing the notebook and dataset.

```bash
python -m pip install -r requirements.txt
python -m jupyterlab
```

Cartopy may download geographic background data when maps are first rendered, so internet access may be needed at that stage.

## Running the workflow

Open `ISC_Implementation.ipynb`, select the Python environment containing the dependencies, and execute the cells in order.

1. Load the GeoPackage.
2. Visualize the 22 predictors and known mineralization locations.
3. Map positive and negative labels against geological provinces.
4. Train and evaluate the two modelling strategies using five-fold cross-validation.
5. Plot ROC, SR, ISC, and alpha-sensitivity curves from saved evaluation results.
6. Map the final prospectivity scores for Set A and Set B.
7. Combine the two prospectivity maps into a two-row figure.

The evaluation-plotting section reads saved results and can be rerun after modelling has completed. The mapping section requires the `cube` object containing the final prospectivity scores.

## Modelling and evaluation settings

| Setting | Current notebook configuration |
| --- | --- |
| Predictors | `F_1`–`F_22` |
| Base classifier | Random Forest |
| Ensemble members | 10 per fitted ensemble |
| Cross-validation | Five folds with separately randomized positive and negative groups |
| Positive folds | Shared between Set A and Set B |
| Random seed | 42, with derived seeds for individual operations |
| Exploration coverage | Number of selected cells divided by the total number of study cells |
| Alpha values | 50 equally spaced values from 0 to 2.5, inclusive |
| Reported evaluation | Mean fold curves and mean fold AUC values |

ROC evaluation uses held-out positive and negative cells. SR evaluation measures the recovery of held-out positive cells against coverage calculated over the full study grid, including unlabelled cells. ISC combines exploration coverage and the held-out false-positive rate while retaining the held-out true-positive rate on the vertical axis.

Positive and negative folds are assigned randomly. The evaluation, therefore, concerns held-out cells within the study region. Final mapping ensembles are subsequently fitted using the available labels for each strategy.

## Generated outputs

The notebook saves evaluation tables, curve summaries, cross-validation scores, and final prospectivity scores in `ModelingResults/`. Principal outputs include

- `cv_summary_metrics.csv`
- `cv_fold_metrics.csv`
- `pooled_oof_roc_metrics.csv`
- `cv_alpha_sensitivity.csv`
- `evaluation_curve_summaries.pkl`
- `cube_with_cv_scores.pkl`
- `cube_with_cv_and_final_scores.pkl`
- `prospectivity_model_A.npy` and `prospectivity_model_B.npy`, when final fitting is enabled

Evaluation figures and prospectivity maps are saved in the notebook's working directory by the current implementation. Full-grid modelling and high-resolution figure generation require sufficient memory and processing time. Hardware requirements and runtime will be documented after a clean-environment run.

## Reproducibility

Fixed random seeds are defined in the notebook. Exact package versions and the configuration used for the manuscript results should accompany the published release. The current notebook specifies 10 ensemble members, which should be checked against the manuscript before publication.

## Citation

Citation metadata will be added in `CITATION.cff`. The manuscript citation will be updated following publication.

## Licence

REPRODUCTION AND DISTRIBUTION TERMS

Unless a specific exception is identified, material may be reproduced
wholly or partly, in any medium, free of charge and without additional
permission for personal or public non-commercial purposes.

When reproducing material:

- Take reasonable care to reproduce it accurately.
- Identify its complete title and author organization.
- Acknowledge NRCan as the publisher of the underlying official work and
  make clear that the reproduction has no NRCan affiliation or endorsement.

Commercial reproduction or distribution requires prior written permission
from Natural Resources Canada. Requests may be directed to:
copyright-droitdauteur@nrcan-rncan.gc.ca 

## Contact

Mohammad Parsa

mohammad.parsasadr@nrcan-rncan.gc.ca


[README.md](https://github.com/user-attachments/files/35036052/README.md)
# ISC
Integrated Spatial–Classification evaluation for mineral prospectivity mapping.
