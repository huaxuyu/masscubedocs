---
title: "feature_evaluation"
weight: 1
---

## Overview

This module provides tools for evaluating the quality of detected features in untargeted metabolomics data. The quality metrics include Gaussian similarity, noise level, and asymmetry factor, which can help assess the reliability and robustness of detected peaks.

## Functions

### calculate_gaussian_similarity

`calculate_gaussian_similarity(x, y)`

Calculates the Gaussian similarity of a peak by comparing its shape to a Gaussian distribution (Pearson product-moment correlation coefficients).

**Parameters:**

- `x` (numpy array): Retention time values of the peak.
- `y` (numpy array): Intensity values of the peak.

**Returns:**

- `similarity` (float): Gaussian similarity score, where higher values indicate better similarity to a Gaussian distribution.

### calculate_noise_level

`calculate_noise_level(y, rel_int_tol=0.05)`

Calculates the noise level of a peak by observing the intensity fluctuations in the peak.

**Parameters:**

- `y` (numpy array): Intensity values of the peak.
- `rel_int_tol` (float): Relative intensity tolerance to the base peak.

**Returns:**

- `noise_level` (float): Noise level, reflecting the signal fluctuation.

### calculate_asymmetry_factor

`calculate_asymmetry_factor(y)`

Calculates the asymmetry factor of the peak at 10% of the peak height.

**Parameters:**

- `y` (numpy array): Intensity values of the peak.

**Returns:**

- `asymmetry_factor` (float): Asymmetry factor, indicating the peak shape asymmetry.
