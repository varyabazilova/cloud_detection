# Cloud detection on Sentinel-2 images

Per-pixel cloud detection using CatBoost on the manually labelled Sentinel-2 dataset of Hollstein et al. (2016). The analysis compares random and scene-based sampling, then applies the final model to a real Sentinel-2 image.

## Repository contents

| Path | Contents |
|---|---|
| `cloud_mapping2.ipynb` | Data overview, validation design, model training, holdout evaluation, figures and results |
| `real_image.ipynb` | Applies the final model to a Sentinel-2 Level-1C image and maps class probabilities |
| `data/` | Input data (not included in Git) |
| `figures/` | Report figures |
| `model/` | Final CatBoost models and input details |
| `results/` | Results tables and supporting CSV files |

## Dependencies

Tested with Python 3.14. Exact package versions from the final run are saved in `results/package_versions.json`.

Install with conda:

```bash
conda create -n clouds -c conda-forge python=3.14 numpy pandas h5py matplotlib scipy scikit-learn catboost cartopy rasterio libgdal-jp2openjpeg jupyterlab ipykernel -y
conda activate clouds
```

## Data

Place these in `data/`:

1. **Training data:** `20170710_s2_manual_classification_data.h5`, from the [Sentinel-2 manual classification repository](https://git.gfz-potsdam.de/EnMAP/sentinel2_manual_classification_clouds/-/tree/master). Licence: CC BY-NC-SA 4.0.
2. **Real image:** Sentinel-2 Level-1C product `S2B_MSIL1C_20261105T045959_N0513_R119_T45RTM_20261105T082324.SAFE`, from the [Copernicus Browser](https://browser.dataspace.copernicus.eu). Level-1C is required, because the model uses top-of-atmosphere reflectance and band B10.

## Running the analysis

Run the notebooks from the repository folder, in this order:

1. `cloud_mapping2.ipynb` creates the figures, results tables and final models.
2. `real_image.ipynb` loads `model/final_scene_4class.cbm` and creates Figure 3.

## Citation for the dataset used

Hollstein, A.; Segl, K.; Guanter, L.; Brell, M.; Enesco, M. Ready-to-Use Methods for the Detection of Clouds, Cirrus, Snow, Shadow, Water and Clear Sky Pixels in Sentinel-2 MSI Images. *Remote Sensing* 2016, 8, 666.
