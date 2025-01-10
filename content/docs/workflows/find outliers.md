---
linkTitle: "Outlier detection"
title: Find outliers
weight: 6
---

## Introduction

Outliers are data files that differ significantly from the rest of the dataset. In MS experiments, outliers can arise due to various factors such as instrument error, sample preparation issues, or biological variation. Identifying and removing outliers before downstream analysis is crucial to avoid misleading results.

_masscube_ evaluates the analytical sequence and reports problematic samples in an unsupervised manner. It assesses the quality of the raw data by analyzing the total peak height of all detected features. Files with a Z-score lower than -2 (by default) are recognized as outliers, ensuring that only high-quality data are included in the downstream analysis.

## How to use

{{% steps %}}

### Step 1. Organize the data

Put all processed raw data files in a folder. The data should be organized in the following structure:

```
my_project
├── single_files
│   ├── sample1.txt
│   ├── sample2.txt
|   └── ...
└── sample_table.csv
```

**Note:** Please provide a sample table to specify the blank samples so that they can be excluded from the outlier detection.

### Step 2. Run the outlier detection

**In the data folder**, open a terminal and run the following command:

```bash
find-outliers
```

### Output

After the processing, you will find the following files and folders in the data folder:

```
my_project
├── single_files
│   ├── sample1.txt
│   ├── sample2.txt
|   └── ...
|── sample_table.csv
└── problematic_files.txt
```

1. `problematic_samples.txt`: a text file containing the names of the problematic samples.
2. `single_files`: a folder containing the feature detection results for each sample.

{{< /steps >}}

## Explanation of the workflow

```python {linenos=table,hl_lines=[],linenostart=1}
def run_evaluation(path=None, zscore_threshold=-2):
    """
    Evaluate the run and report the problematic files.

    Parameters
    ----------
    path : str
        Path to the project directory.
    zscore_threshold : float
        The threshold of z-score for detecting problematic files. Default is -2.
    """
    ...
```

The `run_evaluation` function evaluates the run and reports the problematic files. It checks the quality of the raw data and identifies the problematic samples based on the number of detected features.

The function generates a `problematic_samples.txt` file that lists the names of the problematic samples. Users can further investigate the outliers and decide whether to remove them before downstream analysis.
