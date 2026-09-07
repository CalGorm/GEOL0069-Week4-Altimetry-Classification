# Week 4: Sentinel-3 Altimetry Classification

This repository contains the Week 4 unsupervised-learning analysis of Sentinel-3 SAR altimetry echoes over sea ice.

## Aim

The task is to classify altimetry echoes into sea ice and leads, compare the result with the ESA surface-type classification using a confusion matrix, and examine the average waveform shape and standard deviation for both classes.

## Method

Three waveform-derived features are used:

- backscatter from `sig0_water_20_ku`
- waveform peakiness
- stack standard deviation derived from `rip_20_ku`

Rows containing invalid feature values are removed. The remaining ESA sea-ice and lead observations are standardized and classified using a two-component Gaussian Mixture Model.

The ESA `surf_type_class_20_ku` variable uses:

- 1: sea ice
- 2: lead

The GMM cluster numbers are matched to the physical classes using the ESA classification.

## Results

The GMM classified 12,195 valid echoes:

- sea ice: 8,880
- lead: 3,315

The confusion matrix was:

| ESA classification | GMM sea ice | GMM lead |
|---|---:|---:|
| Sea ice | 8,856 | 22 |
| Lead | 24 | 3,293 |

There were 12,149 agreements and 46 disagreements, giving 99.62% agreement with the ESA classification.

The mean waveform comparison shows a broader and lower-amplitude mean response for sea ice and a sharper, higher-amplitude mean peak for leads. The lead class also has a wider standard-deviation envelope.

## Files

- `notebooks/Week4_Sentinel3_Altimetry_Classification.ipynb` contains the complete analysis.
- `figures/Week4_average_echo_shapes.png` shows the mean waveform and standard-deviation envelope for sea ice and leads.
- `requirements.txt` lists the Python packages used.

## Data

The Sentinel-3 course data are not included in this repository. The notebook expects the supplied Sentinel-3 ZIP file in:

`/content/drive/MyDrive/GEOL0069_Week4/`

The filename should begin with:

`S3A_SR_2_LAN_SI_`

## Reproducibility

The notebook is designed for Google Colab. Mount Google Drive, place the supplied Sentinel-3 ZIP in the Week 4 folder, then run the notebook from top to bottom.
