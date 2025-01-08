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
- `ms2` (str): Representative MS2 spectrum.
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
- `matched_ms2` (str): Matched ms2 spectra.

## Functions

### feature_alignment

`feature_alignment(path: str, params: Params)`

Align the features from multiple processed single files as .txt format.

**Parameters:**

- `path` (str): The path to the feature tables of individual files.
- `params` (Params object): The parameters for alignment including sample names and sample groups.

**Returns:**

- `features` (list of AlignedFeature objects)

### gap_filling

`gap_filling(features, params: Params)`

Fill the gaps for aligned features.

**Parameters:**

- `features` (list of AlignedFeature objects): The aligned features.
- `parameters` (Params object): The parameters used for gap filling.

**Returns:**

- `features` (list of AlignedFeature objects).

### merge_features

`merge_features(features: list, params: Params)`

Clean features by merging features with almost the same m/z and retention time.

**Parameters:**

- `features` (list of AlignedFeature objects): The aligned features.
- `params` (Params object): The parameters used for merging features.

**Returns:**

features (list of AlignedFeature objects).

### convert_features_to_df

`convert_features_to_df(features, sample_names, quant_method="peak_height")`

Convert the aligned features to a DataFrame.

**Parameters:**

- `features` (list of AlignedFeature objects): The aligned features.
- `sample_names` (list): The sample names.
- `quant_method` (str): The quantification method, "peak_height", "peak_area" or "top_average".

**Returns:**

- `feature_table` (pd.DataFrame): The feature DataFrame.

### output_feature_to_msp

`output_feature_to_msp(feature_table, output_path)`

Output MS2 spectra to MSP format.

**Parameters:**

- `feature_table` (pd.DataFrame): The feature table.
- `output_path` (str): The path to the output MSP file.

### output_feature_table

`output_feature_table(feature_table, output_path)`

Output the aligned feature table.

**Parameters:**

- `feature_table` (pd.DataFrame): The aligned feature table.
- `output_path` (str): The path to save the aligned feature table.

### retention_time_correction

`retention_time_correction(mz_ref, rt_ref, mz_arr, rt_arr, mz_tol=0.01, rt_tol=2.0, mode='linear_interpolation', rt_max=None)`

Correct retention times for feature alignment. There are three steps including (1) finding the selected anchors in the given data, (2) creating a model to correct retention times, and (3) correcting retention times.

**Parameters:**

- `mz_ref` (np.array): The m/z values of the selected anchors from another reference file.
- `rt_ref` (np.array): The retention times of the selected anchors from another reference file.
- `mz_arr` (np.array): Feature m/z values in the current file.
- `rt_arr` (np.array): Feature retention times in the current file.
- `mz_tol` (float): The m/z tolerance for selecting anchors.
- `rt_tol` (float): The retention time tolerance for selecting anchors.
- `mode` (str): The mode for retention time correction. Only 'linear_interpolation' is available now.
- `rt_max` (float): End of the retention time range.

**Returns:**

- `rt_arr` (np.array): The corrected retention times.
- `f` (interp1d): The model for retention time correction.

### rt_anchor_selection

`rt_anchor_selection(data_path, num=50, noise_score_tol=0.1, mz_tol=0.01)`

Select retention time anchors from the feature tables. Retention time anchors have unique m/z values and low noise scores. From all candidate features, the top _num_ features with the highest peak heights are selected as anchors.

**Parameters:**

- `data_path` (str): The absolute directory to the feature tables.
- `num` (int): The number of anchors to be selected.
- `noise_score_tol` (float): The noise level for the anchors.
- `mz_tol` (float): The m/z tolerance for selecting anchors.

**Returns:**

- `anchors` (list): A list of anchors (dict) for retention time correction.
