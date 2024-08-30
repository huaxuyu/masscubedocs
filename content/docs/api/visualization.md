---
title: "visualization.py"
weight: 1
---

This module provides a suite of data visualization functions tailored for metabolomics data analysis. It includes tools for plotting base peak chromatograms, extracted ion chromatograms (EIC), histograms, mirror images of MS² spectra, and Principal Component Analysis (PCA) plots. These visualizations aid in the interpretation and quality control of metabolomics experiments.

### **Functions**

#### plot_bpcs

`plot_bpcs(data_list=None, output=None, autocolor=False, show_legend=True)`

Plots overlapped Base Peak Chromatograms (BPC) from a list of MSData objects.

**Parameters:**

- `data_list` (list of MSData objects, optional): A list of MSData objects to be plotted. Each object should contain `ms1_rt_seq` (retention time sequence), `bpc_int` (BPC intensities), and `file_name` attributes.
- `output` (str, optional): Path to save the plot as an image file. If `None`, the plot is displayed instead of being saved.
- `autocolor` (bool, default `False`): If `True`, assigns distinct colors to each BPC using a predefined color list. Otherwise, all BPCs are plotted in black.
- `show_legend` (bool, default `True`): If `True`, displays a legend with the file names.

**Usage:**

```python
plot_bpcs(data_list=ms_data_list, output="bpc_plot.png", autocolor=True, show_legend=True)
```

#### plot_roi

`plot_roi(d, roi, mz_tol=0.01, rt_tol=1.0, output=False, break_scan=None)`

Plots the Extracted Ion Chromatogram (EIC) for a specified region of interest (ROI).

**Parameters:**

- `d` (MSData object): The MSData object containing EIC data.
- `roi` (ROI object): The region of interest containing attributes like `mz`, `rt_seq`, `int_seq`, `scan_idx_seq`, `gaussian_similarity`, `noise_level`, `asymmetry_factor`, and `rt`.
- `mz_tol` (float, default `0.01`): Mass-to-charge ratio (m/z) tolerance for EIC extraction.
- `rt_tol` (float, default `1.0`): Retention time (RT) tolerance around the ROI.
- `output` (str, optional): Path to save the plot as an image file. If `False`, the plot is displayed instead of being saved.
- `break_scan` (int, optional): Scan index at which to break and color the EIC differently.

**Usage:**

```python
plot_roi(ms_data, roi, mz_tol=0.01, rt_tol=1.0, output="roi_plot.png")
```

#### mirror_ms2_from_scans

`mirror_ms2_from_scans(scan1, scan2, output=False)`

Generates a mirror plot of two MS² spectra for comparison.

**Parameters:**

- `scan1` (MS2Scan object): The first MS² scan (experimental).
- `scan2` (MS2Scan object): The second MS² scan (database).
- `output` (str, optional): Path to save the plot as an image file. If `False`, the plot is displayed instead of being saved.

**Usage:**

```python
mirror_ms2_from_scans(scan_exp, scan_db, output="ms2_mirror.png")
```

#### mirror_ms2

`mirror_ms2(precursor_mz1, precursor_mz2, peaks1, peaks2, annotation=None, score=None, output=False)`

Creates a mirror image plot of two MS² spectra based on precursor m/z and fragment peaks.

**Parameters:**

- `precursor_mz1` (float): Precursor m/z of the first spectrum.
- `precursor_mz2` (float): Precursor m/z of the second spectrum.
- `peaks1` (numpy array): Fragment peaks of the first spectrum, shape `(n, 2)` where each row is `[m/z, intensity]`.
- `peaks2` (numpy array): Fragment peaks of the second spectrum, shape `(n, 2)`.
- `annotation` (str, optional): Annotation or name for the second spectrum.
- `score` (float, optional): Similarity score between the two spectra.
- `output` (str, optional): Path to save the plot as an image file. If `False`, the plot is displayed instead of being saved.

**Usage:**

```python
mirror_ms2(precursor1, precursor2, peaks_exp, peaks_db, annotation="Compound A", score=0.85, output="mirror_ms2.png")
```

#### plot_pca

`plot_pca(vecPC1, vecPC2, var_PC1, var_PC2, group_names, colors=None, plot_order=None, output_dir=None)`

Plots a PCA scatter plot with confidence ellipses for each group.

**Parameters:**

- `vecPC1` (array-like): Principal Component 1 scores.
- `vecPC2` (array-like): Principal Component 2 scores.
- `var_PC1` (float): Explained variance ratio for PC1.
- `var_PC2` (float): Explained variance ratio for PC2.
- `group_names` (list or array-like): Group labels for each sample.
- `colors` (list, optional): List of colors for each group. Defaults to a predefined color palette.
- `plot_order` (list, optional): Order in which groups are plotted.
- `output_dir` (str, optional): Path to save the PCA plot as an image file. If `None`, the plot is displayed instead of being saved.

**Usage:**

```python
plot_pca(PC1_scores, PC2_scores, 0.45, 0.30, group_labels, colors=["#FF5050", "#0078F0"], output_dir="pca_plot.png")
```

### **Helper Functions**

#### confidence_ellipse

`confidence_ellipse(x, y, ax, n_std=3.0, facecolor='none', **kwargs)`

Adds a covariance confidence ellipse to a plot.

**Parameters:**

- `x` (array-like): Data for the x-axis.
- `y` (array-like): Data for the y-axis.
- `ax` (matplotlib.axes.Axes): The axes object to draw the ellipse on.
- `n_std` (float, default `3.0`): Number of standard deviations for the ellipse radius.
- `facecolor` (str, default `'none'`): Face color of the ellipse.
- `**kwargs`: Additional keyword arguments for `matplotlib.patches.Ellipse`.

**Usage:**

```python
fig, ax = plt.subplots()
confidence_ellipse(x_data, y_data, ax, n_std=2.0, edgecolor='red')
```

#### random_color_generator

`random_color_generator()`

Generates a random CSS4 color name.

**Returns:**

- `str`: A randomly selected CSS4 color name.

**Usage:**

```python
color = random_color_generator()
```

#### Predefined Color Lists

- `_color_list`: A predefined list of colors used when `autocolor=True` in `plot_bpcs`.

  ```python
  _color_list = ["red", "blue", "green", "orange", "purple", "brown", "pink", "gray", "olive", "cyan"]
  ```

- `COLORS`: A predefined list of hex color codes used in PCA plotting.

  ```python
  COLORS = ["#FF5050", "#0078F0", "#00B050", "#FFC000", "#7030A0", "#FF00FF", "#00B0F0", "#FF0000", "#00FF00", "#0000FF"]
  ```

---

### **Dependencies**

Ensure the following Python packages are installed:

- `matplotlib`
- `numpy`
- `pandas`
- `tqdm`
- `pyteomics`
- Other custom modules:
  - `.annotation` (for `extract_peaks_from_string`)
  - `.raw_data_utils` (for `get_start_time`)
