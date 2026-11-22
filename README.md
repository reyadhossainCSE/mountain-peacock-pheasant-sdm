# Machine Learning-Based Species Distribution Modelling of the Mountain Peacock-Pheasant in Peninsular Malaysia under Data Scarcity

**Md Reyad Hossain¹, Mogana Vadiveloo¹\*, Nurul Syafidah Binti Jamil², Chong Leong Puan³**

¹ Department of Computer Science, Universiti Tunku Abdul Rahman (UTAR), Malaysia
² Department of Digital Economy Technology, Universiti Tunku Abdul Rahman (UTAR), Malaysia
³ Faculty of Forestry and Environment, Universiti Putra Malaysia (UPM), Malaysia

\*Corresponding author: reyadhussain.cse@gmail.com

Presented at the **5th Elsevier International Conference on Machine Learning and Data Engineering (ICMLDE 2026)**, 27–28 November 2026, Dehradun, India. Paper ID: 1243.

---

## Overview

Species distribution models (SDMs) predict where a species is likely to occur by relating field records to environmental predictors. For rare, range-restricted species, records are few and spatially clustered, which can make machine learning (ML) models appear more accurate than they are.

This repository contains the workflow used to model the distribution of the **Mountain Peacock-Pheasant (*Polyplectron inopinatum*)**, a Near Threatened bird confined to the montane forests of the Titiwangsa Range in Peninsular Malaysia, using only **31 presence records**.

## Key findings

- All four ML models reached a mean test AUC between **0.849 and 0.880** under spatial cross-validation, and all outperformed GLM and GAM baselines (AUC 0.838).
- The AUC gap between the best and worst ML model was only **0.031**, smaller than the fold-to-fold variation, so no single model can be called best.
- Random (non-spatial) cross-validation inflated AUC by **0.046 to 0.079** for every model. At this sample size, validation design affects measured performance more than model choice.
- Predicted high suitability forms a narrow corridor along the central Titiwangsa ridge.

## Methodology

1. **Presence data:** eBird records, spatially thinned to one record per 1 km cell (n = 31).
2. **Pseudo-absences:** 10 replicates at a 1:1 ratio, drawn 2–50 km from presence records.
3. **Environmental predictors:** 21 candidates from WorldClim 2.1 (30 arc-seconds) and SRTM elevation and slope, screened with Spearman correlation (|ρ| < 0.7) and VIF (< 10). Seven were retained:

   | Predictor | Description |
   |---|---|
   | Bio4 | Temperature seasonality |
   | Bio7 | Temperature annual range |
   | Bio8 | Mean temperature of wettest quarter |
   | Bio13 | Precipitation of wettest month |
   | Bio15 | Precipitation seasonality |
   | Bio17 | Precipitation of driest quarter |
   | Slope | Terrain slope (from SRTM) |

4. **Models:** MaxEnt, Random Forest, Support Vector Machine, XGBoost and a rank-averaged ensemble, with GLM and GAM as statistical baselines.
5. **Validation:** Checkerboard2 spatial cross-validation (0.509° blocks), giving 40 outer test sets per model. A size-matched random 4-fold split was used only to measure optimism.
6. **Metrics:** AUC, binned Boyce index, sensitivity and specificity.

## Repository structure

<!-- Update this to match the files you actually upload -->

```
├── README.md
├── requirements.txt
├── notebooks/        # analysis notebooks
├── src/              # preprocessing, modelling and evaluation scripts
├── figures/          # figures used in the paper and poster
└── poster/           # ICMLDE 2026 poster (PDF)
```

## Requirements

Python 3 with the packages listed in `requirements.txt`, including:

- `elapid` (MaxEnt)
- `scikit-learn` (Random Forest, SVM)
- `xgboost`
- `numpy`, `pandas`, `geopandas`, `rasterio`

Install with:

```bash
pip install -r requirements.txt
```

## Data

The data are **not included** in this repository.

- **Occurrence records:** eBird Basic Dataset, available on request from the Cornell Lab of Ornithology at https://ebird.org/data/download
- **Climate data:** WorldClim 2.1, https://www.worldclim.org
- **Elevation:** SRTM digital elevation model

Download the data from these sources and place them in a `data/` folder before running the code.

## Citation

If you use this work, please cite:

```
Hossain MR, Vadiveloo M, Jamil NSB, Puan CL. Machine Learning-Based Species
Distribution Modelling of the Mountain Peacock-Pheasant in Peninsular Malaysia
under Data Scarcity. In: Proceedings of the 5th International Conference on
Machine Learning and Data Engineering (ICMLDE 2026). Procedia Computer Science.
2026. (DOI to be added)
```

## License

<!-- Choose a license when creating the repository, e.g. MIT, and update this section -->

This project is released under the MIT License. See `LICENSE` for details.

## Contact

For questions, please contact Md Reyad Hossain (reyadhussain.cse@gmail.com).
