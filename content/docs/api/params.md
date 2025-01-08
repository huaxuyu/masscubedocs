---
title: "params"
weight: 1
---

## Overview

The `params` module defines a class `Params` to store and manage parameters for mass spectrometry data processing. The class provides methods to read parameters from a CSV file, set default parameters based on the type of mass spectrometer and ionization mode, check the validity of parameters, and output parameters to a file. The module also includes a function `find_ms_info` to determine the type of mass spectrometer and ionization mode from a raw file.

## Classes

### `Params`

A class to store and manage parameters for mass spectrometry data processing.

**Attributes:**

- `sample_names` (list): Sample names without extension.
- `sample_abs_paths` (list): Absolute paths of the raw MS data.
- `sample_metadata` (DataFrame): Sample metadata.
- `project_dir` (str): Project directory.
- `sample_dir` (str): Directory for the raw MS data.
- `single_file_dir` (str): Directory for the single file output.
- `tmp_file_dir` (str): Directory for the intermediate file output.
- `ms2_matching_dir` (str): Directory for the MS2 matching output.
- `bpc_dir` (str): Directory for the base peak chromatogram output.
- `project_file_dir` (str): Directory for the project files.
- `normalization_dir` (str): Directory for the normalization output.
- `statistics_dir` (str): Directory for the statistical analysis output.
- `problematic_files` (dict): Problematic files.
- `file_name` (str): File name of the raw data.
- `file_path` (str): Absolute path of the raw data.
- `ion_mode` (str): MS ion mode.
- `ms_type` (str): Type of MS.
- `is_centroid` (bool): Whether the raw data is centroid data.
- `file_format` (str): File type in lower case.
- `time` (datetime): When the data file was acquired.
- `scan_time_unit` (str): Time unit of the scan time.
- `mz_lower_limit` (float): Lower limit of m/z in Da.
- `mz_upper_limit` (float): Upper limit of m/z in Da.
- `rt_lower_limit` (float): Lower limit of RT in minutes.
- `rt_upper_limit` (float): Upper limit of RT in minutes.
- `scan_levels` (list): Scan levels to be read.
- `centroid_mz_tol` (float): m/z tolerance for centroiding.
- `ms1_abs_int_tol` (float): Absolute intensity threshold for MS1.
- `ms2_abs_int_tol` (float): Absolute intensity threshold for MS2.
- `ms2_rel_int_tol` (float): Relative intensity threshold to base peak for MS2.
- `precursor_mz_offset` (float): Offset for MS2 m/z range in Da.
- `mz_tol_ms1` (float): m/z tolerance for MS1.
- `mz_tol_ms2` (float): m/z tolerance for MS2.
- `feature_gap_tol` (int): Gap tolerance within a feature.
- `batch_size` (int): Batch size for parallel processing.
- `percent_cpu_to_use` (float): Percentage of CPU to use.
- `group_features_single_file` (bool): Whether to group features in a single file.
- `scan_scan_cor_tol` (float): Scan-to-scan correlation tolerance for feature grouping.
- `mz_tol_feature_grouping` (float): m/z tolerance for feature grouping.
- `rt_tol_feature_grouping` (float): RT tolerance for feature grouping.
- `valid_charge_states` (list): Valid charge states for feature grouping.
- `mz_tol_alignment` (float): m/z tolerance for alignment.
- `rt_tol_alignment` (float): RT tolerance for alignment.
- `correct_rt` (bool): Whether to perform RT correction.
- `scan_number_cutoff` (int): Feature with non-zero scan number greater than the cutoff will be aligned.
- `detection_rate_cutoff` (float): Features detected need to be >rate\*(qc+sample).
- `merge_features` (bool): Whether to merge features with almost the same m/z and RT.
- `mz_tol_merge_features` (float): m/z tolerance for merging features.
- `rt_tol_merge_features` (float): RT tolerance for merging features.
- `group_features_after_alignment` (bool): Whether to group features after alignment.
- `fill_gaps` (bool): Whether to fill the gaps in the aligned features.
- `gap_filling_method` (str): Method for gap filling.
- `gap_filling_rt_window` (float): RT window for finding local maximum.
- `ms2_library_path` (str): Path to the MS2 library.
- `ms2_sim_tol` (float): MS2 similarity tolerance.
- `fuzzy_search` (bool): Whether to perform fuzzy search.
- `sample_normalization` (bool): Whether to normalize the data based on total sample amount/concentration.
- `sample_norm_method` (str): Sample normalization method.
- `signal_normalization` (bool): Whether to run feature-wised normalization to correct systematic signal drift.
- `signal_norm_method` (str): Normalization method for signal drift.
- `run_statistics` (bool): Whether to perform statistical analysis.
- `plot_bpc` (bool): Whether to plot base peak chromatograms.
- `plot_ms2` (bool): Whether to plot mirror plots for MS2 matching.
- `plot_normalization` (bool): Whether to plot the normalization results.
- `by_group_name` (str): Group name for classifier building.
- `output_single_file` (bool): Whether to output the processed individual files to a csv file.
- `output_ms1_scans` (bool): Whether to output all MS1 scans to a pickle file for faster data reloading.
- `output_aligned_file` (bool): Whether to output aligned features to a csv file.
- `quant_method` (str): Value for quantification and output.

**Methods:**

- `read_parameters_from_csv(path)`: Read parameters from a CSV file.
- `read_sample_metadata(path)`: Read sample metadata from a CSV file.
- `_untargeted_metabolomics_workflow_preparation()`: Prepare the parameters for the untargeted metabolomics workflow.
- `set_default(ms_type, ion_mode)`: Set the parameters by the type of MS.
- `check_parameters()`: Check if the parameters are correct using `PARAMETER_RAGES`.
- `output_parameters(path, format="json")`: Output the parameters to a file.

## Functions

### find_ms_info

`find_ms_info(file_name)`

Find the type of mass spectrometer and ionization mode from the raw file.

**Parameters:**

- `file_name` (str): The file name of the raw file.

**Returns:**

- `ms_type` (str): The type of MS, "orbitrap", "qtof", "tripletof" or "others".
- `ion_mode` (str): The ion mode, "positive" or "negative".
- `centroid` (bool): Whether the data is centroid data.

## Constants

### valid parameter ranges

`PARAMETER_RAGES`

A dictionary of valid parameter ranges.

```python {linenos=table,hl_lines=[],linenostar=1}
PARAMETER_RAGES = {
    "mz_lower_limit": (0.0, 100000.0),
    "mz_upper_limit": (0.0, 100000.0),
    "rt_lower_limit": (0.0, 10000.0),
    "rt_upper_limit": (0.0, 10000.0),
    "centroid_mz_tol": (0.0, 0.1),
    "ms1_abs_int_tol": (0, 1e10),
    "ms2_abs_int_tol": (0, 1e10),
    "ms2_rel_int_tol": (0.0, 1.0),
    "precursor_mz_offset": (0.0, 100000.0),
    "mz_tol_ms1": (0.0, 0.02),
    "mz_tol_ms2": (0.0, 0.02),
    "feature_gap_tol": (0, 100),
    "scan_scan_cor_tol": (0.0, 1.0),
    "mz_tol_alignment": (0.0, 0.02),
    "rt_tol_alignment": (0.0, 2.0),
    "scan_number_cutoff": (0, 100),
    "detection_rate_cutoff": (0.0, 1.0),
    "mz_tol_merge_features": (0.0, 0.02),
    "rt_tol_merge_features": (0.0, 0.5),
    "ms2_sim_tol": (0.0, 1.0)
}
```

### default parameters

`PARAMETER_DEFAULT`

A dictionary of default parameters.

```python {linenos=table,hl_lines=[],linenostar=1}
PARAMETER_DEFAULT = {
    "mz_lower_limit": 0.0,
    "mz_upper_limit": 100000.0,
    "rt_lower_limit": 0.0,
    "rt_upper_limit": 10000.0,
    "centroid_mz_tol": 0.005,
    "ms1_abs_int_tol": 1000.0,
    "ms2_abs_int_tol": 500,
    "ms2_rel_int_tol": 0.01,
    "precursor_mz_offset": 2.0,
    "mz_tol_ms1": 0.01,
    "mz_tol_ms2": 0.015,
    "feature_gap_tol": 30,
    "scan_scan_cor_tol": 0.7,
    "mz_tol_alignment": 0.01,
    "rt_tol_alignment": 0.2,
    "scan_number_cutoff": 5,
    "detection_rate_cutoff": 0.1,
    "mz_tol_merge_features": 0.01,
    "rt_tol_merge_features": 0.05,
    "ms2_sim_tol": 0.7
}
```
