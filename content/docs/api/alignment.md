---
title: "alignment"
weight: 1
---

## Overview

This module provides functionality for aligning metabolic features from different samples in mass spectrometry data.

- **Feature alignment**: Align features across different samples, considering parameters like m/z tolerance and retention time tolerance.
- **Gap filling**: Fill in missing features across aligned samples using various strategies.
- **Merge features**: Clean feature table by merging features with almost the same m/z and retention time.
- **Retention time correction**: Correct retention times to align features more accurately.
- **Output feature table**: Save the aligned features to a file.

---

## Functions

### feature_alignment

`feature_alignment(path: str, params: Params)`

Align the features from multiple processed single files as .txt format.

**Parameters:**

- `path` (str): The path to the feature tables of individual files.
- `params` (Params object): The parameters for alignment including sample names and sample groups.

**Returns:**

- `features` (list of AlignedFeature objects)

---

### gap_filling

`gap_filling(features, params: Params)`

Fill the gaps for aligned features.

**Parameters:**

- `features` (list of AlignedFeature objects): The aligned features.
- `parameters` (Params object): The parameters used for gap filling.

**Returns:**

- `features` (list of AlignedFeature objects).

---

### merge_features

`merge_features(features: list, params: Params)`

Clean features by merging features with almost the same m/z and retention time.

**Parameters:**

- `features` (list of AlignedFeature objects): The aligned features.
- `params` (Params object): The parameters used for merging features.

**Returns:**

features (list of AlignedFeature objects).

---

### output_feature_table

`output_feature_table(feature_table, output_path)`

Outputs the aligned feature table.

**Parameters:**

- `feature_table` (DataFrame): The aligned feature table.
- `output_path` (str): The path where the aligned feature table will be saved.

---

### retention_time_correction

`retention_time_correction(mz_ref, rt_ref, mz_arr, rt_arr, mz_tol=0.01, rt_tol=2.0, mode='linear_interpolation', rt_max=None)`

To correct retention times for feature alignment.

There are three steps:

1. Find the selected anchors in the given data.
2. Create a model to correct retention times.
3. Correct retention times.

**Parameters:**

- `mz_ref` (np.array): The m/z values of the selected anchors from another reference file.
- `rt_ref` (np.array): The retention times of the selected anchors from another reference file.
- `mz_arr` (np.array): Feature m/z values in the current file.
- `rt_arr` (np.array): Feature retention times in the current file.
- `mz_tol` (float): The m/z tolerance for selecting anchors.
- `rt_tol` (float): The retention time tolerance for selecting anchors.
- `mode` (str): The mode for retention time correction. Not used now.
- `rt_max` (float): End of the retention time range.
- `return_model` (bool): Whether to return the model for retention time correction.

**Returns:**

- `rt_arr` (np.array): The corrected retention times.
- `f` (interp1d): The model for retention time correction.

---

### rt_anchor_selection

`rt_anchor_selection(data_path, num=50, noise_score_tol=0.1, mz_tol=0.01)`

Retention time anchors have unique m/z values and low noise scores. From all candidate features, the top _num_ features with the highest peak heights are selected as anchors.

**Parameters:**

- `data_path` (str): The absolute directory to the feature tables.
- `num` (int): The number of anchors to be selected.
- `noise_score_tol` (float): The noise level for the anchors. Suggestions: 0.3 or lower.
- `mz_tol` (float): The m/z tolerance for selecting anchors.

**Returns:**

- `anchors` (list): A list of anchors (dict) for retention time correction.

### split_to_train_test

`split_to_train_test(array, interval=0.1)`

Split the selected anchors into training and testing sets. Not used in the current version.

**Parameters:**

- `array` (numpy.ndarray): The retention times of the selected anchors.
- `interval` (float): The time interval for splitting the anchors (default 0.1).

**Returns:**

- `train_idx` (list): Indices of the training set.
- `test_idx` (list): Indices of the testing set.

---

## Classes

### `AlignedFeature`

A class to model a feature in mass spectrometry data. Generally, a feature is defined as a unique pair of m/z and retention time.

**Attributes:**

- `feature_id_arr` (np.array): Feature ID from individual files (-1 if not detected or gap filled).
- `mz_arr` (np.array): m/z values.
- `rt_arr` (np.array): Retention times.
- `scan_idx_arr` (np.array): Scan index of the peak apex.
- `peak_height_arr` (np.array): Peak height.
- `peak_area_arr` (np.array): Peak area.
- `top_average_arr` (np.array): Average of the highest three intensities.
- `ms2_seq` (list): Representative MS2 spectrum from each file (default: highest total intensity).
- `length_arr` (np.array): Length (i.e. non-zero scans in the peak).
- `gaussian_similarity_arr` (np.array): Gaussian similarity.
- `noise_score_arr` (np.array): Noise score.
- `asymmetry_factor_arr` (np.array): Asymmetry factor.
- `sse_arr` (np.array): Squared error to the smoothed curve.
- `is_segmented_arr` (np.array): Whether the peak is segmented.
- `id` (int): Index of the feature.
- `feature_group_id` (int): Feature group ID.
- `mz` (float): m/z.
- `rt` (float): Retention time.
- `reference_file` (str): The reference file with the highest peak height.
- `reference_scan_idx` (int): The scan index of the peak apex from the reference file.
- `highest_intensity` (float): The highest peak height from individual files (which is the reference file).
- `ms2` (list): Representative MS2 spectrum.
- `ms2_reference_file` (str): The reference file for the representative MS2 spectrum.
- `gaussian_similarity` (float): Gaussian similarity from the reference file.
- `noise_score` (float): Noise level from the reference file.
- `asymmetry_factor` (float): Asymmetry factor from the reference file.
- `detection_rate` (float): Number of detected files / total number of files (blank not included).
- `detection_rate_gap_filled` (float): Number of detected files after gap filling / total number of files (blank not included).
- `charge_state` (int): Charge state.
- `is_isotope` (bool): Whether it is an isotope.
- `isotope_signals` (list): Isotope signals [[m/z, intensity], ...].
- `is_in_source_fragment` (bool): Whether it is an in-source fragment.
- `adduct_type` (str): Adduct type.
- `annotation_algorithm` (str): Annotation algorithm. Not used now.
- `search_mode` (str): 'identity search', 'fuzzy search', or 'mzrt_search'.
- `similarity` (float): Similarity score (0-1).
- `annotation` (str): Name of annotated compound.
- `formula` (str): Molecular formula.
- `matched_peak_number` (int): Number of matched peaks.
- `smiles` (str): SMILES.
- `inchikey` (str): InChIKey.
- `matched_precursor_mz` (float): Matched precursor m/z.
- `matched_adduct_type` (str): Matched adduct type.
- `matched_ms2` (list): Matched ms2 spectra.

---

This documentation should serve as a comprehensive guide for understanding and using the code. You can further enhance it by adding specific examples, diagrams, or more in-depth explanations if needed.
