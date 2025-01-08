---
title: "feature_grouping"
weight: 1
---

## Overview

The `feature_grouping` module provides functions to group features based on their m/z values, retention times, MS2 data, and scan-to-scan correlation. The module is designed for untargeted metabolomics workflows to group features that may represent the same compound, isotopes, in-source fragments, or adducts. The functions in this module are used to group features based on the reference file or within a single file.

## Functions

### group_features_after_alignment

`group_features_after_alignment(features, params: Params)`

Groups features after alignment based on the reference file. This function requires reloading the raw data to examine the scan-to-scan correlation between features. The annotated feature groups are stored in the `feature_group_id` attribute of the AlignedFeature objects.

**Parameters:**

- `features` (list): A list of AlignedFeature objects.
- `params` (Params object): A Params object that contains the parameters for feature grouping.

### group_features_single_file

`group_features_single_file(d)`

Groups features from a single file based on the m/z, retention time, MS2, and scan-to-scan correlation. The annotated feature groups are stored in the `feature_group_id` attribute of the Feature objects.

**Parameters:**

- `d` (MSData object): An MSData object containing the detected ROIs to be grouped.

### generate_search_dict

`generate_search_dict(feature, adduct_form, ion_mode)`

Generates a search dictionary for feature grouping based on the adduct form and ionization mode.

**Parameters:**

- `feature` (Feature object): The feature object to be grouped.
- `adduct_form` (str): The adduct form of the feature.
- `ion_mode` (str): The ionization mode, either "positive" or "negative".

**Returns:**

- `dict`: A dictionary containing the possible adducts and in-source fragments.

### find_isotope_signals

`find_isotope_signals(mz, signals, mz_tol=0.015, charge_state=1, num=5)`

Finds isotope patterns from the MS1 signals based on the m/z value and intensity.

**Parameters:**

- `mz` (float): The m/z value of the feature.
- `signals` (np.array): The MS1 signals as [[m/z, intensity], ...].
- `mz_tol` (float): The m/z tolerance to find isotopes (default 0.015 Da).
- `charge_state` (int): The charge state of the feature (default 1).
- `num` (int): The maximum number of isotopes to be found (default 5).

**Returns:**

- `numpy.array`: The m/z and intensity of the isotopes.

### scan_to_scan_cor_intensity

`scan_to_scan_cor_intensity(a, b)`

Calculates the scan-to-scan correlation between two features using Pearson correlation based on their intensity profiles.

**Parameters:**

- `a` (np.array): Intensity array of the first m/z.
- `b` (np.array): Intensity array of the second m/z.

**Returns:**

- `float`: The scan-to-scan correlation between the two features.

### scan_to_scan_correlation

`scan_to_scan_correlation(feature_a, feature_b)`

Calculates the scan-to-scan correlation between two features using Pearson correlation based on their intensity profiles.

**Parameters:**

- `feature_a` (Feature object): The first feature object.
- `feature_b` (Feature object): The second feature object.

**Returns:**

- `float`: The scan-to-scan correlation between the two features.

### get_charge_state

`get_charge_state(mz_seq, valid_charge_states=[1,2])`

Determines the charge state of the isotopes based on the m/z sequence.

**Parameters:**

- `mz_seq` (list): A list of m/z values of isotopes.
- `valid_charge_states` (list): A list of valid charge states (default [1,2]).

**Returns:**

- `int`: The charge state of the isotopes.

## Constants

### `ADDUCT_POS`

A dictionary of positive adducts with the adduct form as the key and the m/z shift, charge state, and multiplier as the values.

### `ADDUCT_NEG`

A dictionary of negative adducts with the adduct form as the key and the m/z shift, charge state, and multiplier as the values.
