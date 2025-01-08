---
title: "feature_detection"
weight: 1
---

## Overview

Untargeted feature detection.

## Classes

### `Feature`

A class to store a feature characterized by a unique pair of m/z and retention time.

**Attributes:**

- `rt_seq` (list of float): Retention time sequence.
- `signals` (list): Signal sequence organized as [[m/z, intensity], ...].
- `scan_idx_seq` (list of int): Scan index sequence.
- `ms2_seq` (list): MS2 spectra.
- `gap_counter` (int): Counter for the number of consecutive zeros in the peak tail.

- `id` (int): Feature ID.
- `feature_group_id` (int): Peak group ID.
- `mz` (float): m/z value.
- `rt` (float): Retention time.
- `scan_idx` (int): Scan index of the peak apex.
- `peak_height` (float): Peak height.
- `peak_area` (float): Peak area.
- `top_average` (float): Average of the highest three intensities.
- `ms2` (object): Representative MS2 spectrum.
- `length` (int): Number of valid scans in the feature.
- `gaussian_similarity` (float): Gaussian similarity.
- `noise_score` (float): Noise score.
- `asymmetry_factor` (float): Asymmetry factor.
- `sse` (float): Squared error to the smoothed curve.
- `is_segmented` (bool): Indicates if the feature is segmented.
- `is_isotope` (bool): Indicates if the feature is an isotope.
- `charge_state` (int): Charge state of the feature.
- `isotope_signals` (list): Isotope signals [[m/z, intensity], ...].
- `is_in_source_fragment` (bool): Indicates if the feature is an in-source fragment.
- `adduct_type` (str): Adduct type.
- `annotation_algorithm` (str): Annotation algorithm.
- `search_mode` (str): Search mode ('identity search', 'fuzzy search', or 'mzrt_search').
- `similarity` (float): Similarity score (0-1).
- `annotation` (str): Name of annotated compound.
- `formula` (str): Molecular formula.
- `matched_peak_number` (int): Number of matched peaks.
- `smiles` (str): SMILES notation.
- `inchikey` (str): InChIKey notation.
- `matched_precursor_mz` (float): Matched precursor m/z.
- `matched_ms2` (object): Matched MS2 spectra.
- `matched_adduct_type` (str): Matched adduct type.

**Methods:**

- `extend(self, rt, signal, scan_idx)`: Extends the chromatographic peak with new data points.
- `get_mz_error(self)`: Calculates the 3\*sigma error of the feature's m/z.
- `get_rt_error(self)`: Calculates the 3\*sigma error of the feature's retention time.
- `summarize(self, ph=True, pa=True, ta=True, g_score=True, n_score=True, a_score=True)`: Summarizes the feature by calculating summary statistics.
- `subset(self, start, end, summarize=True)`: Keeps a subset of the feature based on start and end positions.

## Functions

### `detect_features`

`detect_features(d)`

Detects features in the MS data.

**Parameters:**

- `d` (MSData object): An object that contains the MS data.

**Returns:**

- `final_features` (list of `Feature` objects): A list of detected features.

### `segment_feature`

`segment_feature(feature, sigma=1.2, prominence_ratio=0.05, distance=10, peak_height_tol=1000, length_tol=5, sse_tol=0.5)`

Segments a feature into multiple features based on edge detection.

**Parameters:**

- `feature` (`Feature` object): The feature to segment.
- `sigma` (float): The sigma value for the Gaussian filter. DFault is 1.2.
- `prominence_ratio` (float): The prominence ratio for finding peaks. Default is 0.05.
- `distance` (int): The minimum distance between peaks. Default is 10.
- `peak_height_tol` (float): The peak height tolerance for segmentation.
- `length_tol` (int): The length tolerance for segmentation. Default is 5.
- `sse_tol` (float): The squared error tolerance for segmentation. Default is 0.5.

**Returns:**

- `segmented_features` (list of `Feature` objects): A list of segmented features.

Please see the source code for more internal functions.
