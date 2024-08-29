# CMI-PB 3rd Public Challenge Data Preparation

This repository contains the codebase for processing and normalizing the training dataset used in the 3rd CMI-PB Public Challenge. The dataset comprises three multi-omics datasets (from 2020, 2021, and 2022) and the challenge dataset (2023). The data require careful processing and normalization to generate computable matrices suitable for model development. While data processing and normalization approaches can vary depending on user preferences, the CMI-PB team has provided a standardized data processing method inspired by the approach used in the 2nd CMI-PB challenge.

The codebase is available on GitHub: [CMI-PB 3rd Public Challenge Data Prep](https://github.com/CMI-PB/cmi-pb-3rd-public-challenge-data-prep). If you have specific questions, please reach out via the Solutions Center.

## Download and Read Public Challenge Data

The data files for the Public CMI-PB challenge can be accessed on the CMI-PB website: [Download Public Challenge Data](https://www.cmi-pb.org/downloads/cmipb_challenge_datasets/current/3rd_challenge/raw_datasets/). Experimental (raw) datasets provide captured the immune response dynamics before and after booster vaccination. The datasets are available as direct file downloads or as R data objects. For our notebook, we recommend downloading the data as R data objects, which include both demographic metadata and experimental data such as:

- **Plasma Antibody Titers**: Measured against Tdap at all time points using the Luminex assay.
- **Plasma Cytokine Concentrations by Olink**: Analyzed using the Olink assay.
- **Plasma Cytokine Concentrations by Legendplex**: Analyzed using the Legendplex assay.
- **PBMC Gene Expression**: RNAseq analysis of bulk peripheral blood mononuclear cells (PBMCs).
- **PBMC Cell Frequency**: Analysis of PBMC subset frequencies.
- **T Cell Activation**: Assessed using the FluoroSpot assay.
- **T Cell Polarization**: Assessed using the AIM assay.

## Step 1: Data Harmonization
- **Standardization of Data Formats**: Ensuring that all datasets are in the same format, including consistent units, feature names, and sample identifiers.
- **Feature Matching**: Ensuring that the same features (e.g., genes, proteins) are being compared across datasets. The 2020 dataset contains more or different features compared to the 2021, 2022, and 2023 datasets. We aimed to extract the maximum overlapping information from these datasets.

Harmonized datasets can be directly used to test different data normalization and batch effect correction methods.

## Step 2: Data Normalization, Imputation, and Batch Effect Correction
- **Data Imputation**: Handling missing data in a way that does not introduce bias is essential when merging datasets with different levels of missingness. We used `impute.knn()` to impute missing data.
- **Normalization**: Adjusting the data to account for differences in measurement scales across different datasets. We used the median baseline value of each feature in each dataset as the normalization factor.
- **Identifying Batch Effects**: Methods like principal component analysis (PCA) are used to identify and visualize batch effects in the data. Batch effects often manifest as clusters in PCA plots that correspond to different batches.
- **Correcting Batch Effects**: We used the ComBat algorithm to correct batch effects in the data.

### Note
These processed datasets are intended to guide contestants through data harmonization and batch effect correction. However, we recognize that many contestants have developed their own data-processing pipelines in previous CMI-PB contests.


