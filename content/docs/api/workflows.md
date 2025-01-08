---
title: "workflows"
weight: 1
---

## Overview

This module provides premade data processing workflows for untargeted metabolomics analysis. The workflows include feature detection, alignment, annotation, normalization, and statistical analysis. The module also includes functions for batch file processing and evaluating the data quality of raw files.

## Functions

### process_single_file

`process_single_file(file_name, params=None, segment_feature=True, group_features=False, evaluate_peak_shape=True, annotate_ms2=False, ms2_library_path=None, output_dir=None)`

Performs untargeted feature detection for a single file.

**Parameters:**

- `file_name` (str): Path to the raw file.
- `params` (Params object, optional): Parameters for feature detection. If `None`, the default parameters are used based on the type of mass spectrometer.
- `segment_feature` (bool, default `True`): Whether to segment the feature to peaks for distinguishing possible isomers.
- `group_features` (bool, default `False`): Whether to group features by isotopes, adducts, and in-source fragments.
- `evaluate_peak_shape` (bool, default `True`): Whether to evaluate the peak shape by calculating noise score and asymmetry factor.
- `annotate_ms2` (bool, default `False`): Whether to annotate MS2 spectra.
- `ms2_library_path` (str, optional): Path to the MS2 library.
- `output_dir` (str, optional): The output directory for the single file. If `None`, the output is saved to the same directory as the raw file.

**Returns:**

- `d` (MSData object): An MSData object containing the processed data.

**Usage:**

```python
# use default parameters for processing a single file
result = feature_detection("sample.mzML")
```

### untargeted_metabolomics_workflow

`untargeted_metabolomics_workflow(path=None, return_results=False, only_process_single_files=False, return_params_only=False)`

The untargeted metabolomics workflow.

**Parameters:**

- `path` (str, optional): The working directory. If `None`, the current working directory is used.
- `return_results` (bool, default `False`): Whether to return the results.
- `only_process_single_files` (bool, default `False`): Whether to only process the single files.
- `return_params_only` (bool, default `False`): Whether to return the parameters only.

**Returns:**

- `features` (list): A list of features.
- `params` (Params object): Parameters for the workflow.

**Usage:**

```python
untargeted_metabolomics_workflow(path="/path/to/project")
```

### batch_file_processing

`batch_file_processing(path=None, segment_feature=True, group_features=False, evaluate_peak_shape=True, annotate_ms2=True, ms2_library_path=None, cpu_ratio=0.8, batch_size=100)`

Process single files using default parameters. This function is useful for batch processing of multiple files. Files from different ion modes are allowed, but parameters cannot be specified for individual files, and default parameters are used.

**Parameters:**

- `path` (str, optional): The working directory. If `None`, the current working directory is used.
- `segment_feature` (bool, default `True`): Whether to segment the feature to peaks for distinguishing possible isomers.
- `group_features` (bool, default `False`): Whether to group features by isotopes, adducts, and in-source fragments.
- `evaluate_peak_shape` (bool, default `True`): Whether to evaluate the peak shape by calculating noise score and asymmetry factor.
- `annotate_ms2` (bool, default `True`): Whether to annotate MS2 spectra.
- `ms2_library_path` (str, optional): The path to the MS2 library.
- `cpu_ratio` (float, default `0.8`): The percentage of CPU cores to use.
- `batch_size` (int, default `100`): The number of files to process in each batch.

### run_evaluation

`run_evaluation(path=None, zscore_threshold=-2)`

Evaluate the run and report the problematic files. The path to the project directory should be organized as follows:

```
path
├── single_files
│   ├── sample1.txt
│   ├── sample2.txt
│   └── ...
└── ...
```

where single_files contains the processed files in txt format.

**Parameters:**

- `path` (str, optional): Path to the project directory.
- `zscore_threshold` (float, default `-2`): The threshold of z-score for detecting problematic files.
