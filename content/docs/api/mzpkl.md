---
title: "mzpkl"
weight: 2
---

## Overview

This module defines the structure of the `mzpkl` file format, which is a temporary file format used to store the raw MS data
for faster reloading. The `mzpkl` file format is a pickle file that is organized this way:

```
{
    "name": str, # the name of the file
    "ion_mode": str, # the ion mode of the file
    "ms1_time_arr": np.ndarray, # the time array of the MS1 scans
    "ms1_idx": np.ndarray, # the index array of the MS1 scans
    "ms2_idx": np.ndarray, # the index array of the MS2 scans
    "scans": list of 2D np.ndarray # MS1 and MS2 scans in the file. Each scan is a 2D np.ndarray with shape (n, 2), [[m/z, intensity], ...]
}
```

---

## Functions

### Convert MS Data object to mzpkl

`convert_MSData_to_mzpkl(d, output_dir: str = None)`

Converts an `MSData` object to an `mzpkl` file.

**Parameters:**

- `d` (MSData): The MSData object to be converted.
- `output_dir` (str): The directory where the `mzpkl` file will be saved.

**Output:**

- the converted `mzpkl` file will be saved in the specified directory.
- if the output directory is not specified, the `mzpkl` file will be returned as a dictionary.

### Read mzpkl to MS Data object

`read_mzpkl_to_MSData(d, file_path: str)`

Reads an `mzpkl` file to an `MSData` object.

**Parameters:**

- `d` (MSData): The initiated MSData object without scans data.
- `file_path` (str): The path to the `mzpkl` file.
