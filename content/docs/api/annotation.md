---
title: "annotation.py"
weight: 1
---

This module is designed for annotating metabolites based on their MS/MS spectra. It includes functions for loading MS/MS databases, performing feature annotation, and exporting results. The module supports various input formats and annotation methods, providing flexibility for different workflows.

## Functions

### load_msms_db

`load_msms_db(path)`

Loads the MS/MS database from a specified path, which can be in `.msp`, `.pkl`, or `.json` format.

**Parameters:**

- `path` (str): The path to the MS/MS database.

**Returns:**

- An instance of `FlashEntropySearch` with the loaded database indexed for fast searches.

### feature_annotation

`feature_annotation(features, parameters, num=5)`

Annotates a list of features based on their MS/MS spectra using a loaded MS/MS database.

**Parameters:**

- `features` (list): A list of features to be annotated.
- `parameters` (Params object): An object containing parameters for the annotation workflow.
- `num` (int): The number of top MS/MS spectra to search.

**Returns:**

- `features` (list): The annotated features.

### feature_annotation_mzrt

`feature_annotation_mzrt(features, path, default_adduct="[M+H]+", mz_tol=0.01, rt_tol=0.3)`

Annotates features based on a provided mzrt file, typically in CSV format.

**Parameters:**

- `features` (list): A list of features to be annotated.
- `path` (str): The path to the mzrt file.
- `default_adduct` (str): The default adduct type for annotation.
- `mz_tol` (float): The m/z tolerance for matching.
- `rt_tol` (float): The RT tolerance for matching.

**Returns:**

- `features` (list): The annotated features.

### annotate_rois

`annotate_rois(d)`

Annotates regions of interest (ROIs) within the MS data using their MS/MS spectra and a loaded MS/MS database.

**Parameters:**

- `d` (MSData object): The MS data object containing the detected ROIs.

**Returns:**

- None. The ROIs in the MSData object are annotated in place.

### annotate_ms2

`annotate_ms2(ms2_seq, path)`

Annotates a sequence of MS/MS spectra using a loaded MS/MS database.

**Parameters:**

- `ms2_seq` (list): A list of MS/MS spectra (each can be a Scan object).
- `path` (str): The path to the MS/MS database.

**Returns:**

- `annotations` (list): A list of annotations for each spectrum in the sequence.

### feature_to_feature_search

`feature_to_feature_search(feature_list, sim_tol=0.8)`

Calculates MS2 similarity between features using a hybrid search method, building a similarity matrix.

**Parameters:**

- `feature_list` (list): A list of AlignedFeature objects.
- `sim_tol` (float): The similarity threshold for the feature-to-feature search.

**Returns:**

- `similarity_matrix` (pandas.DataFrame): A DataFrame containing the similarity matrix between features.

### index_feature_list

`index_feature_list(feature_list, return_db=False)`

Indexes a list of features for spectrum entropy search.

**Parameters:**

- `feature_list` (list): A list of AlignedFeature objects.
- `return_db` (bool): Whether to return the indexed database along with the search object.

**Returns:**

- Either an instance of `FlashEntropySearch` or a tuple of (`FlashEntropySearch`, `db`) depending on the `return_db` parameter.

### output_ms2_to_msp

`output_ms2_to_msp(feature_table, output_path)`

Exports MS2 spectra to MSP format.

**Parameters:**

- `feature_table` (pandas.DataFrame): A DataFrame containing the MS2 spectra.
- `output_path` (str): The path to the output MSP file.

**Returns:**

- None. The spectra are written to the specified MSP file.

### extract_peaks_from_string

`extract_peaks_from_string(ms2)`

Extracts peaks from an MS2 spectrum provided as a string.

**Parameters:**

- `ms2` (str): The MS2 spectrum in string format.

**Returns:**

- `peaks` (numpy.array): The peaks extracted as a numpy array.

### \_convert_peaks_to_string

`_convert_peaks_to_string(peaks)`

Converts peaks from a numpy array to a string format suitable for storage or export.

**Parameters:**

- `peaks` (numpy.array): The peaks in numpy array format.

**Returns:**

- `ms2` (str): The peaks converted to a string format.
