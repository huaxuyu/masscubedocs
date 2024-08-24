---
linkTitle: "Outlier detection"
title: Find outliers
weight: 5
---

## Introduction

Outliers are data points that are significantly different from the rest of the data. In metabolomics, outliers can be caused by various reasons, such as instrument error, sample preparation, or biological variation. It is important to identify and remove outliers before downstream analysis to avoid misleading results.

_masscube_ evaluate the analytical sequnce and report the problematic samples in an unsupervised manner. It checks the quality of the raw data and identifies the problematic samples based on the number of detected features.

## How to use

{{% steps %}}

### Step 1. Organize the data

Put all the raw data files in a folder. The data should be organized in the following structure:

```
data
├── sample1.mzML
├── sample2.mzML
└── ...
```

**Note:** do NOT include blank samples in the data folder or provide a sample table to specify the blank samples.

### Step 2. Run the outlier detection

**In the data folder**, open a terminal and run the following command:

```bash
find-outliers
```

### Output

After the processing, you will find the following files and folders in the data folder:

```
data
├── sample1.mzML
├── sample2.mzML
├── ...
├── problematic_samples.txt
```

1. `problematic_samples.txt`: a text file containing the names of the problematic samples.

{{< /steps >}}

## Explanation of the workflow

```python {linenos=table,hl_lines=[],linenostart=1}
def run_evaluation(path):
    """
    Evaluate the run and report the problematic files.

    Parameters
    ----------
    path : str
        Path to the mzML or mzXML files.
    """

    ...
```

The `run_evaluation` function evaluates the run and reports the problematic files. It checks the quality of the raw data and identifies the problematic samples based on the number of detected features.

The function generates a `problematic_samples.txt` file that lists the names of the problematic samples. Users can further investigate the outliers and decide whether to remove them before downstream analysis.

{{% steps %}}

### Step 1. Fast untargeted feature detection

A fast untargeted feature detection algorithm is applied to the raw data. The algorithm automatically applies the default parameters for feature detection based on the metadata of the raw files. Parameters are not needed to be set by the users.

### Step 2. Find outliers

The total number of features detected in each sample is calculated. Samples with total feature numnber deviating from the mean by more than 3 standard deviations are considered as outliers.

### Step 3. Report problematic samples

The names of the problematic samples are saved in the `problematic_samples.txt` file. Users can further investigate the outliers and decide whether to remove them before downstream analysis.

{{% /steps %}}
