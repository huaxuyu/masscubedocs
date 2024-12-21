---
title: "raw_data_utils"
weight: 1
---

This module provides tools for reading and processing raw mass spectrometry (MS) data, specifically in mzML or mzXML format. It includes a class to handle the data, providing functionalities for extracting scans, finding regions of interest (ROIs), generating chromatograms, and more.

## Overview

The main components of this module include:

- **MSData Class**: A class that models a single MS data file, allowing for the extraction, processing, and visualization of MS data.
- **Scan Class**: A class that represents individual MS scans, including both MS1 and MS2 levels.
- **Helper Functions**: Various utility functions to assist in data processing, such as reading files, centroiding data, and finding the best MS2 spectrum.

---

## Classes

### `MSData`

A class that models a single MS file (mzML or mzXML) and processes the raw data.

**Attributes:**

- `file_name` (str): Name of the raw data file without extension.
- `start_time` (datetime): Start acquisition time of the raw data.
- `params` (Params object): Contains the parameters used for processing.
- `scans` (list): A list of `Scan` objects representing each scan in the data.
- `ms1_rt_seq` (numpy array): Retention times of all MS1 scans.
- `bpc_int` (numpy array): Intensity of the Base Peak Chromatogram (BPC).
- `rois` (list): A list of ROI objects.
- `roi_mz_seq` (numpy array): m/z values of all ROIs.
- `roi_rt_seq` (numpy array): Retention time of all ROIs.

**Methods:**

- `__init__(self)`: Initializes the `MSData` object.
- `read_raw_data(self, file_name, params, read_ms2=True, clean_ms2=False, centroid=True)`: Reads raw MS data and extracts MS1 and MS2 scans.
- `extract_scan_mzml(self, spectra, int_tol=0, read_ms2=True, clean_ms2=False, centroid=True)`: Extracts scans from an mzML file.
- `extract_scan_mzxml(self, spectra, int_tol, read_ms2=True, clean_ms2=False, centroid=True)`: Extracts scans from an mzXML file.
- `drop_ion_by_int(self)`: Drops ions by intensity.
- `find_rois(self)`: Identifies ROIs in MS1 scans.
- `cut_rois(self)`: Splits ROIs into smaller pieces.
- `summarize_roi(self, cal_g_score=True, cal_a_score=True)`: Processes ROIs and assigns MS2 spectra.
- `allocate_ms2_to_rois(self)`: Allocates MS2 spectra to ROIs.
- `drop_rois_without_ms2(self)`: Removes ROIs without MS2 spectra.
- `drop_rois_by_length(self, length=5)`: Removes ROIs shorter than a specified length.
- `plot_bpc(self, rt_range=None, label_name=False, output_dir=None)`: Plots the Base Peak Chromatogram (BPC).
- `output_single_file(self, user_defined_output_path=None)`: Generates a CSV report of ROIs.
- `get_eic_data(self, target_mz, target_rt=None, mz_tol=0.005, rt_tol=0.3, rt_range=None)`: Extracts Extracted Ion Chromatogram (EIC) data for a target m/z.
- `plot_eics(self, target_mz_seq, target_rt=None, mz_tol=0.005, rt_tol=0.3, output=None, show_rt_line=True, ylim=None, return_eic_data=False)`: Plots EICs for multiple target m/z values.
- `plot_eic(self, target_mz, target_rt=None, mz_tol=0.005, rt_tol=0.3, output=None, show_rt_line=True, ylim=None, return_eic_data=False)`: Plots the EIC for a single target m/z.
- `find_ms2_by_mzrt(self, mz_target, rt_target, mz_tol=0.01, rt_tol=0.3, return_best=False)`: Finds MS2 scans by precursor m/z and retention time.
- `find_roi_by_mzrt(self, mz_target, rt_target=None, mz_tol=0.01, rt_tol=0.3)`: Finds ROIs by m/z and retention time.
- `find_ms1_scan_by_rt(self, rt_target)`: Finds an MS1 scan by retention time.
- `correct_retention_time(self, f)`: Corrects retention times based on a provided function.
- `plot_roi(self, roi_idx, mz_tol=0.005, rt_range=[0, np.inf], rt_window=None, output=False)`: Plots the EIC for a specific ROI.
- `plot_all_rois(self, output_path, mz_tol=0.01, rt_range=[0, np.inf], rt_window=None)`: Plots the EICs for all ROIs.

### `Scan`

A class that represents an individual MS scan, either MS1 or MS2.

**Attributes:**

- `level` (int): The MS level of the scan (1 or 2).
- `scan` (int): Scan number.
- `rt` (float): Retention time.
- `mz_seq` (numpy array): m/z sequence (for MS1).
- `int_seq` (numpy array): Intensity sequence (for MS1).
- `precursor_mz` (float): Precursor m/z (for MS2).
- `peaks` (numpy array): Product m/z and intensity pairs (for MS2).

**Methods:**

- `__init__(self, level=None, scan=None, rt=None)`: Initializes the `Scan` object.
- `add_info_by_level(self, **kwargs)`: Adds scan information depending on the MS level.
- `show_scan_info(self)`: Prints the scan's information.
- `plot_scan(self, mz_range=None, return_data=False)`: Plots the scan data.

---

## Helper Functions

### `_clean_ms2(ms2, offset=2, int_drop_ratio=0.01)`

Cleans MS/MS spectra by removing ions with m/z greater than a specified offset and by removing ions with low intensity.

**Parameters:**

- `ms2` (Scan object): The MS2 scan to clean.
- `offset` (float): m/z offset for dropping ions.
- `int_drop_ratio` (float): Ratio of the base peak intensity below which ions will be dropped.

### `_centroid(mz_seq, int_seq, mz_tol=0.005)`

Centroids m/z and intensity sequences.

**Parameters:**

- `mz_seq` (numpy array): m/z sequence.
- `int_seq` (numpy array): Intensity sequence.
- `mz_tol` (float): m/z tolerance for centroiding.

### `read_raw_file_to_obj(file_name, params=None, int_tol=1000, centroid=True, read_ms2=True, clean_ms2=False, print_summary=False)`

Reads a raw MS file into an `MSData` object.

**Parameters:**

- `file_name` (str): Name of the raw MS data file.
- `params` (Params object): Parameters for processing.
- `int_tol` (float): Intensity tolerance for ion filtering.
- `centroid` (bool): Whether to centroid the raw data.
- `print_summary` (bool): Whether to print a summary of the data.

**Returns:**

- `d` (MSData object): The processed MSData object.

### `find_best_ms2(ms2_seq)`

Finds the best MS2 spectrum from a list of MS2 spectra based on intensity.

**Parameters:**

- `ms2_seq` (list): List of MS2 spectra.

**Returns:**

- `best_ms2` (Scan object): The MS2 scan with the highest intensity.

### `get_start_time(file_name)`

Extracts the start time of the raw data from the file.

**Parameters:**

- `file_name` (str): Absolute path to the raw data file.

**Returns:**

- `start_time` (datetime): The start acquisition time of the raw data.
