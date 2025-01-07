# PLAX EF Labels Dataset

This repository contains two datasets of EF (ejection fraction) labels for PLAX (parasternal long-axis) echocardiographic videos, derived from the MIMIC-IV-ECHO and MIMIC-IV-Note dataset. These labels were generated through two distinct approaches and are intended for research use only. Each dataset includes labels formatted to align with the MIMIC-IV-ECHO dataset's structure, enabling seamless integration with corresponding echocardiographic files for those with appropriate access to MIMIC-IV.

## Description of Datasets

### 1. Ground Truth Dataset
This dataset contains EF labels derived from clinical notes in the MIMIC-IV-NOTE dataset. Using time-based correlation and GPT-4 NLP, EF values were extracted from discharge summaries and paired with corresponding PLAX videos. After rigorous filtering and validation:
- **Size**: 295 studies.
- **Methodology**:
  - Correlated echocardiography studies and clinical notes within a 1-day window for highest accuracy.
  - Extracted EF values from free-text notes using GPT-4.
  - Validated EF values using a trained A4C model, achieving a mean absolute error (MAE) of 6.64%.
- **Purpose**: Serves as an independent test set for evaluating PLAX EF prediction models.

### 2. Generated Dataset
This dataset contains EF labels generated through the following pipeline:
- **View Classification**: Applied a fine-tuned video view classifier to identify PLAX and A4C views in MIMIC-IV-ECHO.
- **EF Value Generation**:
  - Used a pre-trained A4C model to predict EF values for A4C videos.
  - Averaged EF predictions across A4C videos in each study to assign EF labels to corresponding PLAX videos.
- **Size**: 25,532 videos across 4,822 studies.
- **Purpose**: Enables training of machine learning models for PLAX EF prediction.

## File Format
Both datasets are provided as CSV files with the following columns:
- **subject_group**: Corresponds to the `pXX` group in MIMIC-IV-ECHO.
- **subject_id**: Corresponds to the `pXXXXXXX` ID in MIMIC-IV-ECHO.
- **study_id**: Corresponds to the `sXXXXXXX` ID in MIMIC-IV-ECHO.
- **file_id**: Corresponds to the `XXXX_XXXX` file identifier in MIMIC-IV-ECHO.
- **EF_value**: Ejection fraction value (percentage).

Example row:
```
p10,p10872900,s96990073,96990073_0057,66.43
```

## Usage Instructions
To use these labels:
1. Ensure you have access to the MIMIC-IV-ECHO dataset.
2. Use the `subject_group`, `subject_id`, `study_id`, and `file_id` columns to locate the corresponding DICOM echo files in MIMIC-IV-ECHO.
3. The `EF_value` column provides the EF percentage for the corresponding video.

## Future Updates
In the future, this repository will include:
- EF labels for A4C views.
- Source code for generating labels using the view classifier and A4C model.

## License
This dataset is derived from the MIMIC-IV-ECHO and MIMIC-IV-NOTE datasets. Use of this dataset must comply with the MIMIC-IV Data Use Agreement. The labels are shared under the Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0) license. For full license details, see [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/).

## Citation
As the associated paper has not yet been accepted, citation details will be added later. For now, please credit the repository as:
```
PLAX EF Labels Dataset, [GitHub Repository Link]
```

## References
This dataset is derived from the following publicly available datasets:
- MIMIC-IV-ECHO: Johnson AEW, Pollard TJ, Shen L, et al. (2020). MIMIC-IV Clinical Database. Version 2.0. Available at: https://physionet.org/content/mimic-iv-echo/
- MIMIC-IV-NOTE: Johnson AEW, Pollard TJ, Shen L, et al. (2020). MIMIC-IV Clinical Database. Version 2.0. Available at: https://physionet.org/content/mimic-iv/
Access to the original datasets requires completion of the PhysioNet Data Use Agreement.

