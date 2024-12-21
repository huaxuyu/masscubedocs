---
title: "stats"
weight: 1
---

This module provides functions for performing statistical analysis on metabolomics data, including univariate analysis (t-tests and ANOVA) and multivariate analysis (Principal Component Analysis or PCA).

---

### **Univariate Analysis**

#### statistical_analysis

`statistical_analysis(feature_table, params, before_norm=False)`

Performs statistical analysis on the feature table, including univariate analysis (t-test or ANOVA) and multivariate analysis (PCA).

**Parameters:**

- `feature_table` (pandas DataFrame): The feature table containing metabolomics data.
- `params` (Params object): The parameters for the experiment.
- `before_norm` (bool): Whether the analysis is performed before normalization. Default is `False`.

**Returns:**

- `pandas DataFrame`: The updated feature table with p-values from statistical tests.

#### t_test

`t_test(data_array, individual_sample_groups)`

Performs a t-test on a feature list for two groups.

**Parameters:**

- `data_array` (numpy array): The feature intensities.
- `individual_sample_groups` (list): A list of groups of individual samples.

**Returns:**

- `list`: p-values from the t-test.

#### anova

`anova(data_array, individual_sample_groups)`

Performs ANOVA on a feature list for more than two groups.

**Parameters:**

- `data_array` (numpy array): The feature intensities.
- `individual_sample_groups` (list): A list of groups of individual samples.

**Returns:**

- `list`: p-values from the ANOVA test.

### **Multivariate Analysis**

#### pca_analysis

`pca_analysis(data_array, individual_sample_groups, scaling=True, transformation=True, gapFillingRatio=0.2, output_dir=None, before_norm=False)`

Performs Principal Component Analysis (PCA) on the data.

**Parameters:**

- `data_array` (numpy array): The feature intensities. Features are in rows and samples are in columns.
- `individual_sample_groups` (list): A list of groups of individual samples.
- `scaling` (bool): Whether to scale the data. Default is `True`.
- `transformation` (bool): Whether to transform the data (log10). Default is `True`.
- `gapFillingRatio` (float): The ratio for gap-filling. Default is `0.2`.
- `output_dir` (str): The directory to save the PCA plot. Default is `None`.
- `before_norm` (bool): Whether the analysis is performed before normalization. Default is `False`.

**Returns:**

- `vecPC1, vecPC2, var_PC1, var_PC2`: PCA results including the principal component vectors and their explained variance ratios.
