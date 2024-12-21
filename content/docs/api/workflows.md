---
title: "workflows"
weight: 1
---

This module summarizes several workflows and utilities for processing untargeted metabolomics data using various tools and packages. It provides comprehensive methods for feature detection, feature alignment, annotation, normalization, statistical analysis, and quality control. The workflows are designed to be flexible, allowing for parallel processing, and they include detailed steps for handling data from raw files to final feature tables.

### feature_detection

`feature_detection(file_name, params=None, cal_g_score=True, cal_a_score=True, anno_isotope=True, anno_adduct=True, anno_in_source_fragment=True, annotation=False, ms2_library_path=None, output_dir=None)`

Performs untargeted feature detection from a single file (e.g., `.mzML` or `.mzXML`).

**Parameters:**

- `file_name` (str): Path to the raw data file.
- `params` (Params object, optional): Parameters for feature detection. If `None`, default parameters are used.
- `cal_g_score` (bool, default `True`): Whether to calculate the Gaussian similarity score for each ROI.
- `anno_isotope` (bool, default `True`): Whether to annotate isotopes.
- `anno_adduct` (bool, default `True`): Whether to annotate adducts.
- `anno_in_source_fragment` (bool, default `True`): Whether to annotate in-source fragments.
- `annotation` (bool, default `False`): Whether to annotate MS2 spectra using an MS2 library.
- `ms2_library_path` (str, optional): Path to the MS2 library file.
- `output_dir` (str, optional): Directory to save output files. If `None`, the output is saved in a default location.

**Returns:**

- `d` (MSData object): An MSData object containing processed data.

**Usage:**

```python
result = feature_detection("sample.mzML", params=custom_params, annotation=True, ms2_library_path="library.msp")
```

---

### untargeted_metabolomics_workflow

`untargeted_metabolomics_workflow(path=None, batch_size=100, cpu_ratio=0.8)`

Performs the full untargeted metabolomics workflow, including feature detection, alignment, annotation, normalization, and statistical analysis.

**Parameters:**

- `path` (str, optional): Path to the working directory. If `None`, the current working directory is used.
- `batch_size` (int, default `100`): Number of files to process in each batch.
- `cpu_ratio` (float, default `0.8`): Ratio of CPU cores to use for parallel processing.

**Usage:**

```python
untargeted_metabolomics_workflow(path="/path/to/project", batch_size=50, cpu_ratio=0.9)
```

---

### batch_file_processing

`batch_file_processing(path=None, batch_size=100, cpu_ratio=0.8)`

Processes multiple files in batch mode using the untargeted metabolomics workflow.

**Parameters:**

- `path` (str, optional): Path to the working directory. If `None`, the current working directory is used.
- `batch_size` (int, default `100`): Number of files to process in each batch.
- `cpu_ratio` (float, default `0.8`): Ratio of CPU cores to use for parallel processing.

**Usage:**

```python
batch_file_processing(path="/path/to/project", batch_size=50, cpu_ratio=0.9)
```

---

### Dependencies

Ensure that the following Python packages are installed:

- `os`, `multiprocessing`, `pickle`, `deepcopy`, `pandas`, `numpy`, `tqdm`, `importlib.metadata`, `scipy`, `time`, `json`

The module also relies on several internal modules and functions:

- `MSData`, `get_start_time` from `.raw_data_utils`
- `Params`, `find_ms_info` from `.params`
- `annotate_isotope`, `annotate_adduct`, `annotate_in_source_fragment` from `.feature_grouping`
- `feature_alignment`, `gap_filling`, `output_feature_table` from `.alignment`
- `feature_annotation`, `annotate_rois`, `feature_annotation_mzrt` from `.annotation`
- `sample_normalization` from `.normalization`
- `plot_ms2_matching_from_feature_table` from `.visualization`
- `statistical_analysis` from `.stats`
- `convert_features_to_df`, `output_feature_to_msp` from `.feature_table_utils`

---
