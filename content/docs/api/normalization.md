---
title: "normalization"
weight: 1
---

## Overview

This module provides functions for normalizing data, particularly in the context of mass spectrometry. There are two types of normalization including

1. Sample normalization - to normalize samples with different total amounts/concentrations.
2. Signal normalization - to address the signal drifts in the mass spectrometry data.

## Functions

### sample_normalization

`sample_normalization(feature_table, sample_metadata=None, method='pqn', feature_selection=True)`

Normalizes samples using a feature list, typically excluding blank samples.

**Parameters:**

- `feature_table` (pandas DataFrame): The feature table.
- `sample_metadata` (pd.DataFrame): DataFrame containing sample metadata. See params module for details.
- `method` (str): The method to find the normalization factors. Options:
  - `'pqn'`: Probabilistic Quotient Normalization.
- `feature_selection` (bool): Whether to select high-quality features for normalization. High-quality features have relative standard deviation (RSD) less than 25% in QC samples and average intensity in QC+biological samples greater than 2 fold of the average intensity in blank samples.

**Returns:**

- `pandas DataFrame`: The normalized feature table.

### find_normalization_factors

`find_normalization_factors(array, method='pqn')`

Finds the normalization factors for a data frame.

**Parameters:**

- `array` (numpy array): The data to be normalized.
- `method` (str): The method to find the normalization factors. Options:
  - `'pqn'`: Probabilistic Quotient Normalization.

**Returns:**

- `numpy array`: The normalization factors.

### sample_normalization_by_factors

`sample_normalization_by_factors(array, v)`

Normalizes a data frame by a vector.

**Parameters:**

- `array` (numpy array): The data to be normalized.
- `v` (numpy array): The normalization factor.

**Returns:**

- `numpy array`: The normalized data.

### find_reference_sample

`find_reference_sample(array, method='median_intensity')`

Finds the reference sample for normalization.

**Parameters:**

- `array` (numpy array): The data to be normalized.
- `method` (str): The method to find the reference sample. Options:
  - `'number'`: The reference sample has the most detected features.
  - `'total_intensity'`: The reference sample has the highest total intensity.
  - `'median_intensity'`: The reference sample has the highest median intensity.

**Returns:**

- `int`: The index of the reference sample.

### high_quality_feature_selection

`high_quality_feature_selection(array, is_qc=None, is_blank=None, blank_ratio_tol=0.5, qc_rsd_tol=0.25)`

Selects high-quality features based on provided criteria for normalization.

**Parameters:**

- `array` (numpy array): The data to be normalized. Samples are in columns and features are in rows.
- `is_qc` (numpy array): Boolean array indicating whether a sample is a quality control sample.
- `is_blank` (numpy array): Boolean array indicating whether a sample is a blank sample.
- `blank_ratio_tol` (float): The tolerance of the ratio of the average intensity in blank samples to the average intensity in QC and biological samples.
- `qc_rsd_tol` (float): The tolerance of the relative standard deviation (RSD) in QC samples.

**Returns:**

- `numpy array`: High-quality features. Features are in rows and samples are in columns.
- `numpy array`: The index of the selected features.

### signal_normalization

`signal_normalization(feature_table, sample_metadata, method='lowess', output_plot_path=None)`

Normalizes MS signal drifts based on analytical order.

**Parameters:**

- `feature_table` (pandas DataFrame): The feature table.
- `sample_metadata` (pd.DataFrame): DataFrame containing sample metadata. See params module for details.
- `method` (str): The method to find the normalization factors. Options:
  - `'lowess'`: Locally Weighted Scatterplot Smoothing.
- `output_plot_path` (str): The path to save the normalization plot. If none, no visualization will be generated.

**Returns:**

- `pandas DataFrame`: The normalized feature table.

### lowess_normalization

`lowess_normalization(array, qc_idx, frac=0.07, it=3)`

Normalizes samples using quality control samples.

**Parameters:**

- `array` (numpy array): The data to be normalized.
- `qc_idx` (numpy array of bool): Boolean array indicating whether a sample is a quality control sample. It's length should be the same as the length of array.
- `frac` (float): The fraction of the data used when estimating each y-value (used in lowess).
- `it` (int): The number of residual-based reweightings to perform (used in lowess).

**Returns:**

- 'dict': A dictionary containing the lowess model, the fit curve, and the normalized array: {'model': model, 'fit_curve': y, 'normed_arr': int_arr_corr}
