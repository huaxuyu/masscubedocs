---
title: "annotation.py"
weight: 1
---

## Overview

This module is designed for annotating metabolites based on their m/z, retention time, and MS/MS spectra.

---

## Functions

### load_ms2_db

`load_ms2_db(path)`

Load MS2 database in `pickle`, `json`, or `msp` format.

**Parameters:**

- `path` (str): The path to the MS2 database.

**Returns:**

- `entropy_search` (FlashEntropySearch object): The MS2 database.

### annotate_aligned_features

`annotate_aligned_features(features, params, num=5)`

Annotate feature's MS2 using database.

**Parameters:**

- `features` (list): A list of AlignedFeature objects.
- `params` (Params object): The parameters for the workflow.
- `num` (int): The number of top MS2 spectra to search.

**Returns:**

- `features` (list): A list of AlignedFeature objects with MS2 annotation.

### annotate_features

Annotate features from a single raw data file using MS2 database.

`annotate_features(d, sim_tol=None, fuzzy_search=True, ms2_library_path=None)`

**Parameters:**

- `d` (MSData object): MS data file.
- `sim_tol` (float): The similarity threshold for MS2 annotation. If not specified, the corresponding parameter from the MS data file will be used.
- `fuzzy_search` (bool): Whether to further annotated the unmatched MS2 using fuzzy search.
- `ms2_library_path` (str): The absolute path to the MS2 database. If not specified, the corresponding parameter from the MS data file will be used.

### annotate_ms2

Annotate MS2 spectra using MS2 database.

`annotate_ms2(ms2, ms2_library_path, sim_tol=0.7, fuzzy_search=True)`

**Parameters:**

- `ms2` (Scan object): MS2 spectrum.
- `ms2_library_path` (str): The absolute path to the MS2 database. If not specified, the corresponding parameter from the MS data file will be used.
- `sim_tol` (float): The similarity threshold for MS2 annotation.
- `fuzzy_search` (bool): Whether to further annotated the unmatched MS2 using fuzzy search.

**Returns:**

- `score` (float): The similarity score.
- `matched` (dict): The matched MS2 spectrum.
- `matched_peak_num` (int): The number of matched peaks.
- `search_mode` (str): The search mode, 'identity_search' or 'fuzzy_search'.

### feature_annotation_mzrt

`feature_annotation_mzrt(features, path, mz_tol=0.01, rt_tol=0.3)`

Annotate features based on a mzrt file (only .csv is supported now)

**Parameters:**

- `features` (list): A list of features.
- `path` (str): The path to the mzrt file in csv format.
- `mz_tol` (float): The m/z tolerance for matching.
- `rt_tol` (float): The RT tolerance for matching.

**Returns:**

- `features` (list): A list of features with annotation.

### feature_to_feature_search

`feature_to_feature_search(feature_list)`

Calculate the MS2 similarity between features using fuzzy search.

**Parameters:**

- `feature_list` (list): A list of AlignedFeature objects.

**Returns:**

- `similarity_matrix` (pandas.DataFrame): A DataFrame containing the similarity matrix between features.

### index_feature_list

`index_feature_list(feature_list)`

A helper function to index a list of features for spectrum entropy search.

**Parameters:**

- `feature_list` (list): A list of AlignedFeature objects.

**Returns:**

- `entropy_search` (FlashEntropySearch object): The indexed feature list.

### output_ms2_to_msp

`output_ms2_to_msp(feature_table, output_path)`

Output MS2 spectra to MSP format

**Parameters:**

- `feature_table` (pandas.DataFrame): A DataFrame containing the MS2 spectra.
- `output_path` (str): The path to the output MSP file.
