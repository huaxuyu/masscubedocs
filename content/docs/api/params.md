---
title: "params"
weight: 1
---

This module defines and manages parameters for mass spectrometry data analysis, including feature detection, alignment, normalization, and statistical analysis. It provides functionalities to read, validate, and output parameters, as well as to prepare workflows for untargeted metabolomics.

## Overview

- **Params Class**: A class to store, manage, and validate parameters for various stages of mass spectrometry data processing.
- **Helper Functions**: Functions to determine mass spectrometry (MS) type, ion mode, and to validate parameter ranges.

---

## Classes

### `Params`

A class to store and manage parameters for the project and individual files in mass spectrometry data processing.

**Attributes:**

- **Project-Related:**

  - `project_dir` (str): Project directory.
  - `sample_names` (list of str): List of raw file paths (without extension).
  - `sample_groups` (list of str): List of sample group names.
  - `sample_group_num` (int): Number of sample groups.
  - `sample_dir` (str): Directory for sample information.
  - `single_file_dir` (str): Directory for single file output.
  - `annotation_dir` (str): Directory for annotation output.
  - `chromatogram_dir` (str): Directory for chromatogram output.
  - `statistics_dir` (str): Directory for statistical analysis output.

- **MS Data Acquisition:**

  - `rt_range` (list of float): Retention time range in minutes, default [0.0, 1000.0].
  - `ion_mode` (str): Ionization mode, either "positive" or "negative".

- **Feature Detection:**

  - `mz_tol_ms1` (float): m/z tolerance for MS1, default 0.01.
  - `mz_tol_ms2` (float): m/z tolerance for MS2, default 0.015.
  - `int_tol` (int): Intensity tolerance, default 30000 for Orbitrap and 1000 for other instruments.
  - `roi_gap` (int): Gap within a feature, default 30.
  - `ppr` (float): Peak correlation threshold for feature grouping, default 0.7.

- **Feature Alignment:**

  - `align_mz_tol` (float): m/z tolerance for MS1, default 0.01.
  - `align_rt_tol` (float): Retention time tolerance, default 0.2.
  - `run_rt_correction` (bool): Whether to perform retention time correction, default True.
  - `min_scan_num_for_alignment` (int): Minimum scan number for feature alignment, default 6.

- **Feature Annotation:**

  - `msms_library` (str): Path to the MS/MS library file.
  - `ms2_sim_tol` (float): MS2 similarity tolerance, default 0.7.

- **Normalization:**

  - `run_normalization` (bool): Whether to normalize the data, default False.
  - `normalization_method` (str): Normalization method, default "pqn" (probabilistic quotient normalization).

- **Output:**

  - `output_single_file` (bool): Whether to output processed individual files as CSV, default False.
  - `output_aligned_file` (bool): Whether to output aligned features as CSV, default False.

- **Statistical Analysis:**

  - `run_statistics` (bool): Whether to perform statistical analysis, default False.

- **Visualization:**
  - `plot_bpc` (bool): Whether to plot base peak chromatogram, default False.
  - `plot_ms2` (bool): Whether to plot MS2 mirror plots for matching, default False.

**Methods:**

- `__init__(self)`: Initializes a Params object with default values.
- `read_parameters_from_csv(self, path)`: Reads parameters from a CSV file.
- `_untargeted_metabolomics_workflow_preparation(self)`: Prepares parameters for an untargeted metabolomics workflow.
- `set_default(self, ms_type, ion_mode)`: Sets default parameters based on the type of mass spectrometer and ionization mode.
- `check_parameters(self)`: Validates the parameters using predefined ranges.
- `output_parameters(self, path, format="json")`: Outputs the parameters to a file, currently only supports JSON format.

---

## Functions

`find_ms_info(file_name)`

Determines the type of mass spectrometer and ionization mode from a raw file.

**Parameters:**

- `file_name` (str): The file name of the raw MS data file.

**Returns:**

- `ms_type` (str): The type of mass spectrometer ("orbitrap" or "tof").
- `ion_mode` (str): The ionization mode ("positive" or "negative").
- `centroid` (bool): Whether the data is centroided.

---

## Constants

### `PARAMETER_RAGES`

A dictionary containing the acceptable ranges for various parameters.

- **Keys and Values:**
  - `"rt_start"`: [0.0, 1000.0]
  - `"rt_end"`: [0.0, 1000.0]
  - `"mz_tol_ms1"`: [0.0, 0.02]
  - `"mz_tol_ms2"`: [0.0, 0.02]
  - `"int_tol"`: [0, 1e10]
  - `"roi_gap"`: [0, 50]
  - `"min_scan_num_for_alignment"`: [0, 50]
  - `"align_mz_tol"`: [0.0, 0.02]
  - `"align_rt_tol"`: [0.0, 2.0]
  - `"ppr"`: [0.5, 1.0]
  - `"ms2_sim_tol"`: [0.0, 1.0]

### `PARAMETER_DEFAULT`

A dictionary containing default values for various parameters.

- **Keys and Values:**
  - `"rt_start"`: 0.0
  - `"rt_end"`: 1000.0
  - `"mz_tol_ms1"`: 0.01
  - `"mz_tol_ms2"`: 0.015
  - `"int_tol"`: 30000
  - `"roi_gap"`: 10
  - `"min_scan_num_for_alignment"`: 5
  - `"align_mz_tol"`: 0.01
  - `"align_rt_tol"`: 0.2
  - `"ppr"`: 0.7
  - `"ms2_sim_tol"`: 0.7

---

This documentation provides a clear and detailed overview of the `Params` class and associated functions, which are crucial for managing and validating parameters in mass spectrometry data processing. This should be useful for users who need to configure and customize their data analysis workflows.
