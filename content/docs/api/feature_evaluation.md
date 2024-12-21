---
title: "feature_evaluation"
weight: 1
---

This module provides tools for predicting the quality of mass spectrometry features based on their peak shape. It includes functions for calculating Gaussian similarity, noise level, and asymmetry factor, which are key indicators of peak quality.

## Overview

- **Gaussian Similarity Calculation**: Estimates how closely the shape of a peak matches a Gaussian distribution.
- **Noise Level Calculation**: Measures the level of noise in the peak, which can indicate the reliability of the peak detection.
- **Asymmetry Factor Calculation**: Evaluates the symmetry of a peak, with ideal peaks being more symmetrical.

---

## Functions

### calculate_gaussian_similarity

`calculate_gaussian_similarity(x, y)`

Calculates the similarity between the observed peak shape and a Gaussian shape using a dot product.

**Parameters:**

- `x` (numpy array): Retention time values.
- `y` (numpy array): Intensity values corresponding to the retention times.

**Returns:**

- `similarity` (float): Similarity score, where 1 indicates a perfect Gaussian shape and values closer to 0 indicate less similarity.

### calculate_noise_level

`calculate_noise_level(y, intensity_threshold=0.1)`

Calculates the noise level of a peak by analyzing intensity fluctuations.

**Parameters:**

- `y` (numpy array): Intensity values of the peak.
- `intensity_threshold` (float): Threshold relative to the maximum intensity for considering points in noise calculation (default 0.1).

**Returns:**

- `noise_level` (float): Noise level of the peak, with higher values indicating more noise.

### calculate_asymmetry_factor

`calculate_asymmetry_factor(y)`

Calculates the asymmetry factor of the peak at 10% of the peak height.

**Parameters:**

- `y` (numpy array): Intensity values of the peak.

**Returns:**

- `asymmetry_factor` (float): Asymmetry factor, where values closer to 1 indicate more symmetrical peaks, and values deviating significantly from 1 indicate asymmetry.

---

## Usage

### Gaussian Similarity Calculation

Gaussian similarity is a measure of how closely a detected peak's shape matches a Gaussian distribution. This is useful for assessing the quality of the peak, as Gaussian-shaped peaks are often indicative of well-resolved features in chromatography.

```python
x = np.array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
y = np.array([0, 2, 6, 10, 14, 15, 14, 10, 6, 2])

similarity = calculate_gaussian_similarity(x, y)
print(f"Gaussian Similarity: {similarity}")
```

### Noise Level Calculation

The noise level is calculated by observing the intensity fluctuations in the peak. Peaks with higher noise levels may be less reliable and indicative of poor detection or background noise.

```python
y = np.array([0, 2, 6, 10, 14, 15, 14, 10, 6, 2])

noise_level = calculate_noise_level(y)
print(f"Noise Level: {noise_level}")
```

### Asymmetry Factor Calculation

The asymmetry factor provides insight into the symmetry of the peak, which is another important characteristic of high-quality peaks. Ideal peaks should be symmetrical.

```python
y = np.array([0, 2, 6, 10, 14, 15, 14, 10, 6, 2])

asymmetry_factor = calculate_asymmetry_factor(y)
print(f"Asymmetry Factor: {asymmetry_factor}")
```
