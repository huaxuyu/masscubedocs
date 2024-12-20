---
title: "feature_detection"
weight: 1
---

This module provides tools for detecting features or peaks in mass spectrometry (MS) data. The main functionalities include finding regions of interest (ROIs), cutting ROIs based on intensity thresholds, and calculating various metrics related to the peaks.

## Overview

- **ROI Detection**: Identifies regions of interest in the MS data, capturing significant peaks and their characteristics.
- **ROI Processing**: Provides tools to refine and cut ROIs, calculate peak areas, and evaluate peak quality.
- **Utilities**: Helper functions to support the detection and processing of ROIs.

---

## Functions

### find_rois

`find_rois(d)`

Identifies regions of interest (ROIs) in the MS data.

**Parameters:**

- `d` (MSData object): An object that contains the MS data.

**Returns:**

- `final_rois` (list of `Roi` objects): A list of detected ROIs.

### cut_roi

`cut_roi(r, int_tol=1000, sigma=1.2, prominence_ratio=0.1, distance=5)`

Cuts a region of interest (ROI) into smaller segments based on intensity and peak prominence.

**Parameters:**

- `r` (Roi object): The ROI object to be cut.
- `int_tol` (int): Intensity tolerance for cutting (default 1000).
- `sigma` (float): Sigma value for Gaussian filtering (default 1.2).
- `prominence_ratio` (float): Ratio of prominence used for finding peaks (default 0.1).
- `distance` (int): Minimum distance between peaks (default 5).

**Returns:**

- `cut_rois` (list of `Roi` objects): A list of cut ROIs.

`find_closest_index_ordered(array, target, tol=0.01)`

Finds the index of the closest value in an ordered array.

**Parameters:**

- `array` (list or numpy array): The ordered array to search.
- `target` (float): The target value to find.
- `tol` (float): Tolerance for considering a match (default 0.01).

**Returns:**

- `idx` (int or None): The index of the closest value, or `None` if no suitable match is found.

---

## Classes

### `Roi`

A class to represent a region of interest (ROI) in mass spectrometry data. An ROI typically corresponds to a peak or a group of peaks in a chromatogram.

**Attributes:**

- `id` (int): Identifier for the ROI.
- `scan_idx_seq` (list of int): List of scan indices.
- `rt_seq` (list of float): List of retention times.
- `mz_seq` (list of float): List of m/z values.
- `int_seq` (list of int): List of intensity values.
- `ms2_seq` (list): List of associated MS2 spectra.
- `gap_counter` (int): Counter for the number of gaps in the ROI's tail.
- `mz` (float): m/z value of the ROI peak.
- `rt` (float): Retention time of the ROI peak.
- `scan_number` (int): Number of scans in the ROI.
- `peak_area` (float): Area under the peak.
- `peak_height` (float): Height of the peak.
- `best_ms2` (MS2 object): The best associated MS2 spectrum.
- `length` (int): Length of the ROI in terms of the number of scans.
- `merged` (bool): Indicates if the ROI has been merged with others.
- `gaussian_similarity` (float): Gaussian similarity score of the peak shape.
- `noise_level` (float): Estimated noise level in the ROI.
- `asymmetry_factor` (float): Asymmetry factor of the peak.
- `cut` (bool): Indicates if the ROI has been cut into smaller segments.
- `charge_state` (int): Charge state of the ROI (default 1).
- `is_isotope` (bool): Indicates if the ROI represents an isotope.
- `isotope_mz_seq` (list of float): List of m/z values for isotopes.
- `isotope_int_seq` (list of int): List of intensities for isotopes.
- `isotope_id_seq` (list of int): List of identifiers for isotopes.
- `is_in_source_fragment` (bool): Indicates if the ROI is an in-source fragment.
- `isf_child_roi_id` (list of int): List of child ROI IDs if the ROI is an in-source fragment.
- `isf_parent_roi_id` (int): Parent ROI ID if the ROI is an in-source fragment.
- `adduct_type` (str): Type of adduct, if applicable.
- `adduct_parent_roi_id` (int): Parent ROI ID for the adduct.
- `adduct_child_roi_id` (list of int): List of child ROI IDs for the adduct.
- `annotation` (str): Annotation of the ROI.
- `formula` (str): Molecular formula associated with the ROI.
- `similarity` (float): Similarity score for annotation.
- `matched_peak_number` (int): Number of matched peaks in the ROI.
- `smiles` (str): SMILES notation of the associated molecule.
- `inchikey` (str): InChIKey notation of the associated molecule.

**Methods:**

- `__init__(self, scan_idx, rt, mz, intensity)`: Initializes an ROI with scan index, retention time, m/z, and intensity.
- `extend_roi(self, scan_idx, rt, mz, intensity)`: Extends an ROI with new data points.
- `show_roi_info(self, show_annotation=False)`: Prints information about the ROI.
- `get_mz_error(self)`: Calculates the m/z error (maximum - minimum) of the ROI.
- `find_rt_ph_pa(self)`: Calculates the peak area and height using the trapezoidal rule.
- `find_top_average(self, num=3)`: Finds the peak height by averaging the top three intensities.
- `sum_roi(self, cal_g_score=True, cal_a_score=True)`: Summarizes the ROI, calculating key attributes.
- `subset_roi(self, start, end)`: Subsets the ROI based on provided start and end positions.
