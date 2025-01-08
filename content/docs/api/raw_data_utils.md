---
title: "raw_data_utils"
weight: 1
---

## Overview

The `raw_data_utils` module provides classes and functions for reading and processing raw mass spectrometry (MS) data files. The module supports reading mzML, mzXML, mzjson, and compressed mzjson files. The main class in this module is `MSData`, which models a single MS file and processes the raw data. The module also includes helper functions for cleaning MS/MS spectra, centroiding m/z and intensity sequences, and extracting EIC data.

## Classes

### `MSData`

A class that models a single raw MS data file and processes the raw data.

**Attributes:**

- `scans` (list): A list of `Scan` objects for mass spectra.
- `ms1_idx` (list): Scan indexes of MS1 spectra.
- `ms1_time_arr` (list): Time of MS1 scans.
- `ms2_idx` (list): Scan indexes of MS2 spectra.
- `params` (Params object): A `Params` object that contains all parameters.
- `base_peak_arr` (list): Base peak chromatogram, `[[m/z, intensity], ...]`.
- `features` (list): A list of features.
- `feature_mz_arr` (numpy array): m/z of all ROIs.

**Methods:**

- `read_raw_data(self, file_name, params=None, scan_levels=[1,2], centroid_mz_tol=0.005, ms1_abs_int_tol=None, ms2_abs_int_tol=None, ms2_rel_int_tol=0.01, precursor_mz_offset=2)`: Reads raw data from an MS file.
- `extract_scan_mzml(self, scans)`: Extracts all scans from an mzML file.
- `extract_scan_mzxml(self, scans)`: Extracts all scans from an mzXML file.
- `drop_ms1_ions_by_intensity(self, int_tol)`: Drops ions in all MS1 scans by intensity threshold.
- `detect_features(self)`: Runs feature detection.
- `segment_features(self, iteration=2)`: Segments features by edge detection.
- `summarize_features(self, cal_g_score=True, cal_a_score=True)`: Processes features to calculate summary statistics.
- `allocate_ms2_to_features(self, mz_tol=0.015)`: Allocates MS2 scans to ROIs.
- `drop_features_without_ms2(self)`: Drops features without MS2 scans.
- `drop_features_by_length(self, length=5)`: Drops features by length.
- `drop_isotope_features(self)`: Drops features annotated as isotopes.
- `drop_in_source_fragment_features(self)`: Discards in-source fragments.
- `plot_bpc(self, time_range=None, label_name=True, output_dir=None)`: Plots the base peak chromatogram.
- `output_single_file(self, output_path=None)`: Generates a report for features in csv format.
- `get_eic_data(self, target_mz, target_rt=None, mz_tol=0.005, rt_tol=0.3, rt_range=None)`: Gets the EIC data of a target m/z.
- `plot_eics(self, target_mz_arr, target_rt=None, mz_tol=0.005, rt_tol=0.3, rt_range=None, output_file_name=None, show_target_rt=True, ylim: list=None, return_eic_data=False)`: Plots multiple EICs in a single plot.
- `find_ms2_by_mzrt(self, mz_target, rt_target, mz_tol=0.01, rt_tol=0.3, return_best=False)`: Finds MS2 scan by precursor m/z and retention time.
- `find_feature_by_mzrt(self, mz_target, rt_target=None, mz_tol=0.01, rt_tol=0.3)`: Finds feature by precursor m/z and retention time.
- `find_ms1_scan_by_rt(self, rt_target)`: Finds the nearest n MS1 scan by retention time.
- `correct_retention_time(self, f)`: Corrects retention time.
- `plot_feature(self, feature_idx, mz_tol=0.005, rt_range=[0, np.inf], rt_window=None, output=False)`: Plots EIC of a ROI.

### `Scan`

A class that models a single mass spectrum scan.

**Attributes:**

- `level` (int): Level of mass spectrum.
- `id` (int): Scan ID.
- `scan_time` (float): Scan time.
- `signals` (numpy array): m/z and intensity signals.
- `precursor_mz` (float): Precursor m/z.

## Functions

### clean_signals

`clean_signals(signals, mz_range=None, intensity_range=None)`

Cleans signals by removing ions outside specified m/z and intensity ranges.

**Parameters:**

- `signals` (numpy array): m/z and intensity signals.
- `mz_range` (list): m/z range [start, end].
- `intensity_range` (list): Intensity range [min, max].

**Returns:**

- `cleaned_signals` (numpy array): Cleaned m/z and intensity signals.

### centroid_signals

`centroid_signals(signals, mz_tol)`

Centroids m/z and intensity signals.

**Parameters:**

- `signals` (numpy array): m/z and intensity signals.
- `mz_tol` (float): m/z tolerance.

**Returns:**

- `centroided_signals` (numpy array): Centroided m/z and intensity signals.

### segment_feature

`segment_feature(feature, peak_height_tol, distance)`

Segments a feature by edge detection.

**Parameters:**

- `feature` (Feature object): A feature.
- `peak_height_tol` (int): Peak height tolerance.
- `distance` (int): Distance.

**Returns:**

- `segmented_features` (list): Segmented features.

### detect_features

`detect_features(ms_data)`

Detects features in MS data.

**Parameters:**

- `ms_data` (MSData object): An MSData object.

**Returns:**

- `features` (list): Detected features.

### find_best_ms2

`find_best_ms2(ms2_seq)`

Finds the best MS2 scan with the highest total intensity.

**Parameters:**

- `ms2_seq` (list): A list of MS2 scans.

**Returns:**

- `best_ms2` (Scan object): The best MS2 scan.
