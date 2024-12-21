---
title: "normalization"
weight: 1
---

This module provides functions for normalizing metabolomics data, focusing on two main types of normalization: **Sample Normalization** and **Signal Normalization**. These methods help address issues like varying sample concentrations and signal drift in mass spectrometry data.

## Sample Normalization

These functions focus on normalizing samples to account for differences in total amounts or concentrations between samples.

### find_normalization_factors

`find_normalization_factors(array, method='pqn')`

Finds normalization factors for a dataset based on the specified method.

**Parameters:**

- `array` (numpy array): The data to be normalized.
- `method` (str): The method to find the normalization factors. Options:
  - `'pqn'`: Probabilistic Quotient Normalization.

**Returns:**

- `numpy array`: Normalization factors.

### sample_normalization_by_factors

`sample_normalization_by_factors(array, v)`

Normalizes the data based on the provided normalization factors.

**Parameters:**

- `array` (numpy array): The data to be normalized.
- `v` (numpy array): The normalization factors.

**Returns:**

- `numpy array`: The normalized data.

### find_reference_sample

`find_reference_sample(array, method='median_intensity')`

Finds the reference sample for normalization.

**Parameters:**

- `array` (numpy array): The data to be normalized.
- `method` (str): The method to find the reference sample. Options:
  - `'number'`: The sample with the most detected features.
  - `'total_intensity'`: The sample with the highest total intensity.
  - `'median_intensity'`: The sample with the highest median intensity.

**Returns:**

- `int`: The index of the reference sample.

### sample_normalization

`sample_normalization(feature_table, individual_sample_groups, method='pqn')`

Normalizes samples using a feature list, typically excluding blank samples.

**Parameters:**

- `feature_table` (pandas DataFrame): The feature table.
- `individual_sample_groups` (list): List of groups for individual samples. Blank samples will be skipped.
- `method` (str): The method to find the normalization factors. Options:
  - `'pqn'`: Probabilistic Quotient Normalization.

**Returns:**

- `pandas DataFrame`: The normalized feature table.

## Signal Normalization

These functions focus on correcting signal drift in the data, particularly important in mass spectrometry.

### qc_normalization

`qc_normalization(array, order, qc_idx, batch_idx=None, method='lowess')`

Normalizes samples using quality control (QC) samples to correct for signal drift.

**Parameters:**

- `array` (numpy array): The data to be normalized. Samples are in columns, and features are in rows.
- `order` (list): The order of the samples. It should have the same length as the number of samples.
- `qc_idx` (list): The index of the quality control samples.
- `batch_idx` (list): The index of the batches. Not used currently.
- `method` (str): The method to normalize the data. Options:
  - `'lowess'`: Locally Weighted Scatterplot Smoothing.

**Returns:**

- `numpy array`: The normalized data.
