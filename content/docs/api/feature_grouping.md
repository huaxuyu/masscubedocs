---
title: "feature_grouping"
weight: 1
---

This module provides functionalities to group metabolic features in mass spectrometry data based on unique compounds. The module includes methods to annotate isotopes, adducts, and in-source fragments, which are essential for accurate interpretation of mass spectrometry data.

## Overview

- **Isotope Annotation**: Identifies isotopic patterns within the data and annotates features that represent different isotopes of the same compound.
- **Adduct Annotation**: Detects and annotates different adducts of a compound, which can appear due to various ionization processes.
- **In-Source Fragment Annotation**: Identifies and annotates fragments that may form in the ion source, ensuring they are correctly associated with their parent compounds.

---

## Functions

### annotate_isotope

`annotate_isotope(d, mz_tol=0.015, rt_tol=0.1, valid_intensity_ratio_range=[0.001, 1.2], charge_state_range=[1, 2])`

Annotates isotopes in the MS data by comparing m/z and retention time values.

**Parameters:**

- `d` (MSData object): An MSData object containing the detected regions of interest (ROIs).
- `mz_tol` (float): m/z tolerance for identifying isotopes (default 0.015).
- `rt_tol` (float): Retention time tolerance for identifying isotopes (default 0.1).
- `valid_intensity_ratio_range` (list): Valid intensity ratio range between isotopes (default [0.001, 1.2]).
- `charge_state_range` (list): The range of charge states to consider for isotopes (default [1, 2]).

**Returns:**

- None. The function directly annotates the `d.rois` list with isotope information.

### annotate_in_source_fragment

`annotate_in_source_fragment(d, mz_tol=0.01, rt_tol=0.05)`

Annotates in-source fragments by analyzing the MS data, focusing on peaks that may represent fragments of parent compounds.

**Parameters:**

- `d` (MSData object): An MSData object containing the detected ROIs.
- `mz_tol` (float): m/z tolerance for identifying in-source fragments (default 0.01).
- `rt_tol` (float): Retention time tolerance for identifying in-source fragments (default 0.05).

**Returns:**

- None. The function annotates the `d.rois` list with in-source fragment information.

### `annotate_adduct(d, mz_tol=0.01, rt_tol=0.05)`

Annotates adducts within the MS data by comparing m/z values and retention times, assuming different adducts of the same compound.

**Parameters:**

- `d` (MSData object): An MSData object containing the detected ROIs.
- `mz_tol` (float): m/z tolerance for identifying adducts (default 0.01).
- `rt_tol` (float): Retention time tolerance for identifying adducts (default 0.05).

**Returns:**

- None. The function annotates the `d.rois` list with adduct information.

### peak_peak_correlation

`peak_peak_correlation(roi1, roi2)`

Calculates the peak-peak correlation between two ROIs based on their intensity profiles.

**Parameters:**

- `roi1` (ROI object): The first ROI to compare.
- `roi2` (ROI object): The second ROI to compare.

**Returns:**

- `pp_cor` (float): The peak-peak correlation value, where values close to 1 indicate strong correlation.

### get_charge_state

`get_charge_state(mz_seq)`

Determines the charge state of a compound based on the difference between m/z values in its isotope series.

**Parameters:**

- `mz_seq` (list of floats): A list of m/z values representing the isotope series.

**Returns:**

- `charge_state` (int): The inferred charge state, either 1 or 2.

---

## Usage

### Isotope Annotation

To annotate isotopes in your mass spectrometry data:

```python
annotate_isotope(d, mz_tol=0.01, rt_tol=0.1)
```

### In-Source Fragment Annotation

To annotate in-source fragments:

```python
annotate_in_source_fragment(d, mz_tol=0.01, rt_tol=0.05)
```

### Adduct Annotation

To annotate adducts in the MS data:

```python
annotate_adduct(d, mz_tol=0.01, rt_tol=0.05)
```

---

## Constants

### `_ADDUCT_MASS_DIFFERENCE_POS_AGAINST_H`

A dictionary containing the mass differences for common adducts in positive ion mode, relative to the proton adduct `[M+H]+`.

### `_ADDUCT_MASS_DIFFERENCE_NEG_AGAINST_H`

A dictionary containing the mass differences for common adducts in negative ion mode, relative to the deprotonated molecule `[M-H]-`.
