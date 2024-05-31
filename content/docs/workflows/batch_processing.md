---
linkTitle: "Batch processing"
title: Untargeted single file processing in batch mode
weight: 4
---

## Introduction

Processing each raw LC-MS data individually can be useful for further customized analysis. In this workflow, we introduce how to process single files in batch mode using *masscube*. Note, the processed files will not be aligned across samples. Users may employ the [OneClick untargeted metabolomics workflow](/docs/quickstart) for comprehensive data processing.

## How to use

{{% steps %}}

### Organize the data

Similar to the untargeted metabolomics workflow, the data should be organized in the following structure:

You need <u>two components</u> for the project plus <u>one MS/MS library</u> for annotation.

In your project folder (e.g. **my_project**), you need to prepare the following components:

```
my_project
├── data
│   ├── sample1.mzML
│   ├── sample2.mzML
|   └── ...
└── parameters.csv
```

### Processing

**In the project folder**, open a terminal and run the following command:

```bash
process-files
```

### Output

After the processing, you will find the following files and folders in the project folder:

```
project/
├── data
├── parameters.csv
├── project.mc
├── single_file_output
│   ├── sample1.txt
│   ├── sample2.txt
│   └── ...
├── chromatogram
│   ├── sample1.png
│   ├── sample2.png
│   └── ...
├── ...
```

1. `project.mc` file: the project file of *masscube*.
2. `single_file_output` folder: a folder containing the feature table for each sample.
3. `chromatogram` folder: a folder containing the chromatogram for each sample.

{{% /steps %}}

## Explainations of the workflow

```python {linenos=table,hl_lines=[],linenostart=1}
def batch_file_processing(path=None, batch_size=100, cpu_ratio=0.8):
    """
    The untargeted metabolomics workflow. See the documentation for details.

    Parameters
    ----------
    path : str
        The working directory. If None, the current working directory is used.
    batch_size : int
        The number of files to be processed in each batch.
    cpu_ratio : float
        The ratio of CPU cores to be used.
    """

    ...
```

{{% steps %}}

### Step 1. Define or load parameters

The parameters are critical for MS data processing. However, setting parameters are often challenging, especially for beginners or scientists who are not familiar with the MS data. 

*masscube* automatically read the MS data and apply the corresponding default parameters. Users can also customize the parameters by providing a parameter file.

### Step 2. Single file processing

Individual files are processed for feature detection, which envolves the detection of peak apex, edges, area, and related MS/MS spectra. It also includes the determination of isotopes, charge states, adducts, and in-source fragments.

To accelerate the processing, *masscube* supports parallel computing for multiple files. By default, the number of threads is set to be the 80% (```cpu_ratio=0.8```) of the total CPU cores so that the computer can still be used for other tasks.

To control the memory usage, the files are processed in batches. The default batch size is 100 (```batch_size=100```).

More details about the feature detection can be found [here](/docs/algorithms/feature_detection).

### Step 3. Data visualization

Users can choose to plot the base peak chromatogram (BPC) to verify possible bad injections or outliers.

{{% /steps %}}
