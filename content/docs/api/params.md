---
linkTitle: "params"
weight: 1
---

# `params`

## Overview

The `params` module defines a class `Params` that stores and manages parameters for **mass spectrometry-based untargeted metabolomics data processing**. It also exposes a helper function `find_ms_info` and two dictionaries of parameter **ranges** and **defaults**.

This documentation is synchronized with the current implementation in `params.py` and reflects **all attributes, methods, behaviors, defaults, and edge cases** present in the code.

## Classes

### `Params`

A configuration container for project-level and file-level processing parameters, including project setup, raw data reading/cleaning, feature detection, grouping, alignment, annotation, normalization, statistics, visualization, and output controls.

## Attributes

### Project & Metadata

- `sample_metadata` _(pandas.DataFrame | None)_ — sample table held in-memory.
- `project_dir` _(str | None)_ — project root directory.
- `sample_dir` _(str | None)_ — directory for raw MS data; set during workflow prep.
- `single_file_dir` _(str | None)_ — outputs for single-file processing.
- `tmp_file_dir` _(str | None)_ — temporary/intermediate files.
- `ms2_matching_dir` _(str | None)_ — MS/MS matching outputs.
- `bpc_dir` _(str | None)_ — base peak chromatogram outputs.
- `project_file_dir` _(str | None)_ — auxiliary project files (sample table with time, etc.).
- `normalization_dir` _(str | None)_ — normalization results.
- `statistics_dir` _(str | None)_ — statistical analysis results.
- `problematic_files` _(dict)_ — problematic files mapping `{file_name: error_message}`.

### Raw Data Reading & Cleaning

- `file_name` _(str | None)_ — file name of the raw data.
- `file_path` _(str | None)_ — absolute path of the raw data.
- `ion_mode` _(str)_ — `"positive"` (default) or `"negative"`.
- `ms_type` _(str | None)_ — `"orbitrap"`, `"qtof"`, `"tripletof"`, or `"others"`.
- `is_centroid` _(bool)_ — whether data is centroided (`True` by default).
- `file_format` _(str | None)_ — lower-case type (`"mzml"`, `"mzxml"`, `"mzjson"`, or `"mzjson.gz"`).
- `scan_time_unit` _(str)_ — `"minute"` (default) or `"second"`.
- `mz_lower_limit` _(float)_ — lower m/z bound (default `0.0`).
- `mz_upper_limit` _(float)_ — upper m/z bound (default `100000.0`).
- `rt_lower_limit` _(float)_ — lower RT bound in minutes (default `0.0`).
- `rt_upper_limit` _(float)_ — upper RT bound in minutes (default `10000.0`).
- `scan_levels` _(list[int])_ — scan levels to read (default `[1, 2]`).
- `centroid_mz_tol` _(float | None)_ — m/z tolerance for centroiding (`0.005` by default; set `None` to disable centroiding).
- `ms1_abs_int_tol` _(float)_ — MS1 absolute intensity threshold (recommend `30000` Orbitrap, `1000` QTOF).
- `ms2_abs_int_tol` _(float)_ — MS2 absolute intensity threshold (recommend `10000` Orbitrap, `500` QTOF).
- `ms2_rel_int_tol` _(float)_ — MS2 relative intensity to base peak (default `0.01`).
- `precursor_mz_offset` _(float)_ — m/z offset for defining MS2 range (default `2.0`).

### Feature Detection

- `mz_tol_ms1` _(float)_ — MS1 m/z tolerance (default `0.01`).
- `mz_tol_ms2` _(float)_ — MS2 m/z tolerance (default `0.015`).
- `feature_gap_tol` _(int)_ — tolerance in **consecutive scans** without signal inside a feature (default **`10`** in `Params`; see note below about `PARAMETER_DEFAULT`).
- `batch_size` _(int)_ — parallel processing batch size (default `100`).
- `percent_cpu_to_use` _(float)_ — fraction of CPU to use (default `0.8`).

### Feature Grouping

- `group_features_single_file` _(bool)_ — group features within a single file (default `False`).
- `scan_scan_cor_tol` _(float)_ — scan-to-scan correlation threshold (default `0.7`).
- `mz_tol_feature_grouping` _(float)_ — m/z tolerance for grouping (default **`0.015`**).
- `rt_tol_feature_grouping` _(float)_ — RT tolerance for grouping (default `0.1`).
- `valid_charge_states` _(list[int])_ — allowed charge states (default `[1]`).

### Feature Alignment

- `mz_tol_alignment` _(float)_ — m/z tolerance for alignment (default `0.01`).
- `rt_tol_alignment` _(float)_ — RT tolerance for alignment (default `0.2`).
- `rt_tol_rt_correction` _(float)_ — **expected max RT shift** for RT correction (default `0.5` min).
- `correct_rt` _(bool)_ — perform RT correction (default `True`).
- `scan_number_cutoff` _(int)_ — minimum non-zero scans to be aligned (default `5`).
- `detection_rate_cutoff` _(float)_ — required detection rate across QC+samples (default `0.1`).
- `merge_features` _(bool)_ — merge near-duplicate features (default `True`).
- `mz_tol_merge_features` _(float)_ — m/z tolerance for merging (default `0.01`).
- `rt_tol_merge_features` _(float)_ — RT tolerance for merging (default **`0.02`**).
- `group_features_after_alignment` _(bool)_ — group after alignment (default **`True`**).
- `fill_gaps` _(bool)_ — fill gaps in aligned features (default `True`).
- `gap_filling_method` _(str)_ — method used in gap filling (default `"local_maximum"`).
- `gap_filling_rt_window` _(float)_ — RT window for finding local maxima (default `0.05` min).
- `isotope_rel_int_limit` _(float)_ — isotope intensity upper limit relative to base peak (default `1.5`).

### Feature Annotation

- `ms2_library_path` _(str | None)_ — path to MS2 library (`.msp` or `.pickle`); set to `None` if not existing.
- `fuzzy_search` _(bool)_ — enable fuzzy search (default `False`).
- `consider_rt` _(bool)_ — consider RT in MS2 matching (default `False`).
- `rt_tol_annotation` _(float)_ — RT tolerance for annotation (default `0.2`).
- `ms2_sim_tol` _(float)_ — MS2 similarity threshold (default `0.7`).
- `spectral_similarity_method` _(str)_ — similarity method (default `"unweighted_entropy"`).

### Normalization

- `sample_normalization` _(bool)_ — sample-wise normalization by total amount/concentration (default `False`).
- `sample_norm_method` _(str)_ — method for sample normalization (default `"pqn"`).
- `signal_normalization` _(bool)_ — feature-wise drift correction (default `False`).
- `signal_norm_method` _(str)_ — drift correction method (default `"lowess"`).

### Statistics

- `run_statistics` _(bool)_ — run statistical analysis (default `False`).

### Visualization

- `plot_bpc` _(bool)_ — plot BPC chromatograms (default `False`).
- `plot_ms2` _(bool)_ — plot MS2 mirror plots (default `False`).
- `plot_normalization` _(bool)_ — plot normalization results (default `False`).

### Classifier Building

- `by_group_name` _(str | None)_ — group name for classifier training (if used).

### Output

- `output_single_file` _(bool)_ — export processed single-file outputs (default `False`; set `True` during workflow prep).
- `output_ms1_scans` _(bool)_ — export all MS1 scans to pickle for fast reloading (default `False`; set `True` during workflow prep).
- `output_aligned_file` _(bool)_ — export aligned features (default `False`; set `True` during workflow prep).
- `quant_method` _(str)_ — `"peak_height"` (default), `"peak_area"`, or `"top_average"`.

## Methods

### `read_parameters_from_csv(path)`

Reads a CSV of key–value pairs and sets attributes. Values convertible to `float` are cast; otherwise, `"true"/"yes"` → `True`, `"false"/"no"` → `False`. Calls `check_parameters()` afterward.

### `read_sample_metadata(path)`

Loads sample metadata from CSV. Lower-cases columns named `"is_qc"` and `"is_blank"`; converts `"yes"/"no"` strings to booleans (otherwise defaults both columns to `False`). Sorts so **QC appear first** and **blanks last**; adds `VALID` and `ABSOLUTE_PATH` columns; stores in `sample_metadata`.

### `_untargeted_metabolomics_workflow_preparation()`

Prepares a project for the **untargeted metabolomics** workflow:

1. Validates `project_dir`; derives standard subdirectories and creates them if missing.
2. Ensures raw data exist in `project_dir/data` (currently auto-detects only **`.mzML`** and **`.mzXML`**).
3. If `sample_table.csv` is missing, disables normalization/statistics and prints notices.
4. If `parameters.csv` is missing, prints notices, infers `(ms_type, ion_mode)` from the first sample via `find_ms_info`, calls `set_default`, and enables `plot_bpc`.
5. Loads sample table if present; otherwise builds from discovered file basenames. Validates presence of raw files, computes acquisition `time` via `get_start_time`, filters invalid, sorts by time, adds sequential `analytical_order`, and assigns batch IDs via `label_batch_id`. Writes `project_files/sample_table_with_time.csv`.
6. Sets output toggles: `output_single_file=True`, `output_ms1_scans=True`, `output_aligned_file=True`.

### `set_default(ms_type, ion_mode)`

For `"orbitrap"`, sets `ms1_abs_int_tol=30000`, `ms2_abs_int_tol=10000`; for others, `ms1_abs_int_tol=1000`, `ms2_abs_int_tol=500`. Also sets `ion_mode`.

### `check_parameters()`

Validates all numeric parameters against `PARAMETER_RAGES`. If a value is **out of range**, it prints a warning and resets that parameter to the value in `PARAMETER_DEFAULT`. If `ms2_library_path` does **not** exist, sets it to `None`. Casts `batch_size` to `int`.

> **Note:** The code refers to `PARAMETER_RAGES` throughout (typo intentional to match the implementation).

### `output_parameters(path, format="json")`

Exports **all** parameters (except `project_dir`) to JSON, including `"MassCube_version"` obtained from `importlib.metadata.version("masscube")`. Only `"json"` is supported.

### `_check_raw_files_in_data_dir()`

Cross-references basenames from `sample_metadata` with files in `sample_dir` (currently only `.mzML`/`.mzXML`), sets `VALID` and populates `ABSOLUTE_PATH` accordingly.

---

## Functions

### `find_ms_info(file_name)`

Reads up to the first 200 lines of an **`.mzML`** or **`.mzXML`** file (lower-cased text) to infer:

- `ms_type`: `"orbitrap"` if it contains `"orbitrap"`/`"q exactive"`, `"tripletof"` if `"tripletof"`, else `"qtof"` if contains `"tof"`.
- `ion_mode`: `"positive"` or `"negative"` if mentioned.
- `centroid`: `True` if `"centroid spectrum"` or `centroided="1"` present.

Returns `(ms_type, ion_mode, centroid)`.

---

## Constants

### `PARAMETER_RAGES` — Valid Ranges

```python
PARAMETER_RAGES = {
    "mz_lower_limit": (0.0, 100000.0),
    "mz_upper_limit": (0.0, 100000.0),
    "rt_lower_limit": (0.0, 10000.0),
    "rt_upper_limit": (0.0, 10000.0),
    "centroid_mz_tol": (0.0, 0.1),
    "ms1_abs_int_tol": (0, 1e10),
    "ms2_abs_int_tol": (0, 1e10),
    "ms2_rel_int_tol": (0.0, 1.0),
    "precursor_mz_offset": (0.0, 100000.0),
    "mz_tol_ms1": (0.0, 0.02),
    "mz_tol_ms2": (0.0, 0.02),
    "feature_gap_tol": (0, 100),
    "scan_scan_cor_tol": (0.0, 1.0),
    "mz_tol_alignment": (0.0, 0.02),
    "rt_tol_alignment": (0.0, 2.0),
    "scan_number_cutoff": (0, 100),
    "detection_rate_cutoff": (0.0, 1.0),
    "mz_tol_merge_features": (0.0, 0.02),
    "rt_tol_merge_features": (0.0, 0.5),
    "ms2_sim_tol": (0.0, 1.0)
}
```

### `PARAMETER_DEFAULT` — Defaults Used on Reset

```python
PARAMETER_DEFAULT = {
    "mz_lower_limit": 0.0,
    "mz_upper_limit": 100000.0,
    "rt_lower_limit": 0.0,
    "rt_upper_limit": 10000.0,
    "centroid_mz_tol": 0.005,
    "ms1_abs_int_tol": 1000.0,
    "ms2_abs_int_tol": 500,
    "ms2_rel_int_tol": 0.01,
    "precursor_mz_offset": 2.0,
    "mz_tol_ms1": 0.01,
    "mz_tol_ms2": 0.015,
    "feature_gap_tol": 30,
    "scan_scan_cor_tol": 0.7,
    "mz_tol_alignment": 0.01,
    "rt_tol_alignment": 0.2,
    "scan_number_cutoff": 5,
    "detection_rate_cutoff": 0.1,
    "mz_tol_merge_features": 0.01,
    "rt_tol_merge_features": 0.05,
    "ms2_sim_tol": 0.7
}
```

> **Discrepancy note:** In the `Params` initializer, `feature_gap_tol` defaults to **`10`**, whereas `PARAMETER_DEFAULT["feature_gap_tol"]` is **`30`**. If `check_parameters()` resets values (due to range violations), it will use the **`30`** from `PARAMETER_DEFAULT`.

---

## Additional Notes & Gotchas

- **Raw file discovery** in workflow prep and path validation currently recognizes only `.mzML` and `.mzXML` files, even though `file_format` supports `"mzjson"`/`"mzjson.gz"` in principle.
- `group_features_after_alignment` is **`True`** in the initializer (despite an inline comment that mentions `False`), and `gap_filling_method` is the string `"local_maximum"`.
- If `ms2_library_path` points to a **non-existent** path, it is automatically set to `None` during parameter checking.
- Exported JSON via `output_parameters()` omits `project_dir` and includes a `"MassCube_version"` field.
- The code consistently uses the identifier `PARAMETER_RAGES` (with a **G**), and method docs reflect that spelling.

---

_This documentation mirrors the current `params.py` implementation._
