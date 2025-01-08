---
title: "utils_functions"
weight: 1
---

## Overview

The `utils_functions` module contains utility functions that are commonly used in the data processing and analysis of mass spectrometry data. The module includes functions for generating a sample table, getting timestamps for individual files, converting chemical formulas to m/z values, extracting signals from MS2 spectrum in string format, and converting signals to string format.

## Functions

### generate_sample_table

`generate_sample_table(path=None, output=True)`

Generate a sample table from the mzML or mzXML files in the specified path. The stucture of the path should be:

```
path
├── data
│   ├── sample1.mzml
│   ├── sample2.mzml
│   └── ...
└── ...
```

**Parameters:**

- `path` : str
  Path to the main directory that contains a subdirectory 'data' with mzML or mzXML files.
- `output` : bool
  If True, output the sample table to a csv file.

**Return:**

- `sample_table` : pandas DataFrame
  A DataFrame with two columns: 'Sample' and 'Groups'.

**Output:**

- `sample_table.csv` : csv file
  A csv file with two columns: 'Sample' and 'Groups' in the specified path.

### get_timestamps

`get_timestamps(path=None, output=True)`

Get timestamps for individual files and sort the files by time. The stucture of the path should be:

```
path
├── data
│   ├── sample1.mzml
│   ├── sample2.mzml
│   └── ...
└── ...
```

**Parameters:**

- `path` : str
  Path to the main directory that contains a subdirectory 'data' with mzML or mzXML files.
- `output` : bool
  If True, output the timestamps to a txt file with two columns: 'file_name' and 'aquisition_time'.

**Return:**

- `file_times` : list
  A list of tuples with two elements: 'file_name' and 'aquisition_time'.

**Output:**

- `timestamps.txt` : txt file
  A txt file with two columns: 'file_name' and 'aquisition_time' in the specified path.

### formula_to_mz

`formula_to_mz(formula, adduct, charge)`

Calculate the m/z value of a molecule given its chemical formula, adduct and charge.

**Parameters:**

- `formula` : str
  Chemical formula of the molecule.
- `adduct` : str
  Adduct of the molecule. The first character should be '+' or '-'. In particular,
  for adduct like [M-H-H2O]-, use '-H3O' or '-H2OH'.
- `charge` : int
  Charge of the molecule. Positive for cations and negative for anions.

**Returns:**

- `mz` : float
  The m/z value of the molecule.

**Examples:**

```python
formula_to_mz("C6H12O6", "+H", 1)
# 181.070665

formula_to_mz("C9H14N3O8P", "-H2OH", -1)
# 304.034010
```

### get_start_time

`get_start_time(file_name)`

Function to get the start time of the raw data.

**Parameters:**

- `file_name` : str
  Absolute path of the raw data.

### extract_signals_from_string

`extract_signals_from_string(ms2)`

Extract signals from MS2 spectrum in string format.

**Parameters:**

- `ms2` : str
  MS2 spectrum in string format. Format: "mz1;intensity1|mz2;intensity2|..."

**Returns:**

- `peaks` : numpy.array
  Peaks in numpy array format: [[mz1, intensity1], [mz2, intensity2], ...]

### convert_signals_to_string

`convert_signals_to_string(signals)`

Convert peaks to string format.

**Parameters:**

- `signals` : numpy.array
  MS2 signals organized as [[mz1, intensity1], [mz2, intensity2], ...]

**Returns:**

- `string` : str
  Converted signals in string format. Format: "mz1;intensity1|mz2;intensity2|..."
