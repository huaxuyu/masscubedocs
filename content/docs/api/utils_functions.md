---
title: "utils_functions.py"
weight: 1
---

This module provides utility functions for metabolomics data processing, including generating sample tables, obtaining timestamps from files, calculating ion masses, and estimating isotope distributions.

### generate_sample_table

`generate_sample_table(path=None, output=True)`

Generates a sample table from the mzML or mzXML files in a specified directory.

**Parameters:**

- `path` (str): The path to the directory containing the 'data' subdirectory with mzML or mzXML files. If not specified, the current working directory is used.
- `output` (bool): If `True`, outputs the sample table to a CSV file.

**Returns:**

- `pandas DataFrame` (if `output=False`): The sample table containing two columns: 'Sample' and 'Groups'.

**Outputs:**

- `sample_table.csv` (if `output=True`): A CSV file with the sample table.

**Usage:**

```python
sample_table = generate_sample_table("/path/to/project", output=True)
```

### get_timestamps

`get_timestamps(path, output=True)`

Obtains timestamps for individual mzML or mzXML files and sorts the files by acquisition time.

**Parameters:**

- `path` (str): The path to the directory containing the 'data' subdirectory with mzML or mzXML files.
- `output` (bool): If `True`, outputs the timestamps to a TXT file.

**Returns:**

- `list` or `pandas DataFrame` (if `output=False`): A list or DataFrame of tuples containing 'file_name' and 'acquisition_time'.

**Outputs:**

- `timestamps.txt` (if `output=True`): A TXT file with the timestamps.

**Usage:**

```python
timestamps = get_timestamps("/path/to/project", output=True)
```
