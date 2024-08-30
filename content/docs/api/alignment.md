---
title: "Alignment.py"
weight: 1
---

This module provides functionality for aligning metabolic features from different samples in mass spectrometry data. Isotopes and in-source fragments are not considered in the alignment process.

## Overview

The main components of this module include:

- **Feature Alignment**: Align features across different samples, considering parameters like m/z tolerance and retention time tolerance.
- **Gap Filling**: Fill in missing features across aligned samples using various strategies.
- **Retention Time Correction**: Correct retention times to align features more accurately.
- **Output**: Save the aligned features to a file.

---

## Functions

`feature_alignment(path, parameters, drop_by_fill_pct_ratio=0.1)`

Aligns features from individual files (.txt) based on m/z and retention time.

**Parameters:**

- `path` (str): The path to the feature tables.
- `parameters` (Params object): The parameters used for alignment, including tolerances and correction settings.
- `drop_by_fill_pct_ratio` (float): The threshold for dropping features based on fill percentage (default 0.1).

**Returns:**

- `feature_table` (DataFrame): The aligned feature table.

`gap_filling(features, parameters, mode='forced_peak_picking')`

Fills the gaps in the aligned feature table using specified strategies.

**Parameters:**

- `features` (list): The aligned features.
- `parameters` (Params object): The parameters used for gap filling.
- `mode` (str): The mode of gap filling (`'forced_peak_picking'` or `'0.1_min_intensity'`).

**Returns:**

- `features` (list): The aligned features with filled gaps.

`output_feature_table(feature_table, output_path)`

Outputs the aligned feature table to a specified file.

**Parameters:**

- `feature_table` (DataFrame): The aligned feature table.
- `output_path` (str): The path where the aligned feature table will be saved.

`retention_time_correction(mz_ref, rt_ref, mz_arr, rt_arr, rt_max=50, mode='linear_interpolation', mz_tol=0.015, rt_tol=2.0, found_marker_ratio=0.4, return_model=False)`

Corrects retention times for feature alignment using selected anchors and a specified correction model.

**Parameters:**

- `mz_ref` (np.array): The m/z values of the reference features.
- `rt_ref` (np.array): The retention times of the reference features.
- `mz_arr` (np.array): The m/z values of the features to be corrected.
- `rt_arr` (np.array): The retention times of the features to be corrected.
- `rt_max` (float): Maximum retention time (default 50).
- `mode` (str): Mode of correction (`'linear_interpolation'` by default).
- `mz_tol` (float): m/z tolerance for selecting anchors.
- `rt_tol` (float): Retention time tolerance for selecting anchors.
- `found_marker_ratio` (float): Ratio of found markers required for correction (default 0.4).
- `return_model` (bool): Whether to return the correction model (default `False`).

**Returns:**

- `rt_corr` (np.array): The corrected retention times.

`rt_anchor_selection(data_list, num=50, noise_tol=0.3, mz_tol=0.01, return_all_anchor=False)`

Selects anchors for retention time correction based on the provided data. Anchors are selected based on intensity, peak shape, and distribution.

**Parameters:**

- `data_list` (list): A list of `MSData` objects or file names of the output `.txt` files.
- `num` (int): Number of anchors to be selected (default 50).
- `noise_tol` (float): Noise level tolerance for selecting anchors (default 0.3).
- `mz_tol` (float): m/z tolerance for anchor selection (default 0.01).
- `return_all_anchor` (bool): Whether to return all anchors (default `False`).

**Returns:**

- `anchors` (list): A list of anchors (m/z and retention times) for retention time correction.

`_split_to_train_test(array, interval=0.3)`

Splits selected anchors into training and testing sets based on a specified time interval.

**Parameters:**

- `array` (numpy.ndarray): The retention times of the selected anchors.
- `interval` (float): The time interval for splitting the anchors (default 0.3).

**Returns:**

- `train_idx` (list): Indices of the training set.
- `test_idx` (list): Indices of the testing set.

---

## Classes

### `Feature`

A class that models a feature in mass spectrometry data, typically defined by a unique pair of m/z and retention time.

**Attributes:**

- `id` (int): Index of the feature.
- `reference_file` (str): The reference file for the feature.
- `mz` (float): m/z value.
- `rt` (float): Retention time.
- `highest_intensity` (float): The highest peak height from individual files.
- `best_ms2` (str): The best MS2 spectrum.
- `gaussian_similarity` (float): Gaussian similarity score.
- `noise_level` (float): Noise level.
- `asymmetry_factor` (float): Asymmetry factor.
- `fill_percentage` (float): Fill percentage across samples.
- `charge_state` (int): Charge state (default 1).
- `is_isotope` (bool): Indicates if the feature is an isotope.
- `isotopes` (list): List of isotopes associated with the feature.
- `is_in_source_fragment` (bool): Indicates if the feature is an in-source fragment.
- `adduct_type` (str): Adduct type.
- `annotation` (str): Annotation of the feature.
- `search_mode` (str): Search mode (`'identity search'`, `'hybrid search'`, `'mzrt_search'`).
- `formula` (str): Molecular formula.
- `similarity` (float): Similarity score (0-1).
- `matched_peak_number` (int): Number of matched peaks.
- `smiles` (str): SMILES notation.
- `inchikey` (str): InChIKey notation.
- `matched_ms2` (str): Matched MS2 spectrum.
- `mz_seq` (numpy array): m/z values from individual files.
- `rt_seq` (numpy array): Retention time values from individual files.
- `peak_height_seq` (numpy array): Peak heights from individual files.
- `peak_area_seq` (numpy array): Peak areas from individual files.
- `ms2_seq` (list): List of best MS2 spectra from individual files.
- `detected_seq` (numpy array): Boolean array indicating detection in individual files.
- `roi_id_seq` (numpy array): ROI IDs from individual files.
- `fold_change` (float): Fold change value.
- `t_test_p` (float): t-test p-value.
- `adjusted_t_test_p` (float): Adjusted t-test p-value.

**Methods:**

- `__init__(self, file_number=1)`: Initializes a `Feature` object.
- `calculate_mzrt(self)`: Calculates the m/z and retention time of the feature by averaging detected values.

---

This documentation should serve as a comprehensive guide for understanding and using the code. You can further enhance it by adding specific examples, diagrams, or more in-depth explanations if needed.
