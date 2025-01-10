---
linkTitle: "Batch processing"
title: Single file processing by applying default parameters depending on the data
weight: 5
---

## Introduction

Processing each raw LC-MS data individually can be useful for further customized analysis. In this workflow, we introduce how to process single files in batch mode using _masscube_. Note, the processed files will not be aligned across samples. Also, files with different ion modes and instruments are allowed in the same batch, as _masscube_ will apply different parameters depending on the data.

## How to use

{{% steps %}}

### Organize the data

Similar to the untargeted metabolomics workflow, the data should be organized in the following structure:

```
my_project
├── data
│   ├── sample1.mzML
│   ├── sample2.mzML
|   └── ...
├── ...
```

You cannot set parameters here.

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

1. `single_file_output` folder: a folder containing the feature table for each sample.
2. `chromatogram` folder: a folder containing the chromatogram for each sample.

{{% /steps %}}

## Explainations of the workflow

```python {linenos=table,hl_lines=[],linenostart=1}
def batch_file_processing(path=None, segment_feature=True, group_features=False, evaluate_peak_shape=True,
                         annotate_ms2=True, ms2_library_path=None, cpu_ratio=0.8, batch_size=100):
    """
    Process single files using default parameters.

    Parameters
    ----------
    path : str
        The working directory. If None, the current working directory is used.
    segment_feature : bool
        Whether to segment the feature to peaks for distinguishing possible isomers. Default is True.
    group_features : bool
        Whether to group features by isotopes, adducts and in-source fragments. Default is True.
    evaluate_peak_shape : bool
        Whether to evaluate the peak shape by calculating noise score and asymmetry factor. Default is True.
    annotate_ms2 : bool
        Whether to annotate MS2 spectra. Default is True.
    ms2_library_path : str
        The path to the MS2 library.
    cpu_ratio : float
        The percentage of CPU cores to use. Default is 0.8.
    batch_size : int
        The number of files to process in each batch. Default is 100.
    """
    ...
```

{{% steps %}}

### Step 1. Single file processing

Individual files are processed for feature detection, which envolves the detection of peak apex, edges, area, and related MS/MS spectra. It also includes the determination of isotopes, charge states, adducts, and in-source fragments.

To accelerate the processing, _masscube_ supports parallel computing for multiple files. By default, the number of threads is set to be the 80% (`cpu_ratio=0.8`) of the total CPU cores so that the computer can still be used for other tasks.

To control the memory usage, the files are processed in batches. The default batch size is 100 (`batch_size=100`).

### Step 2. Data visualization

Users can choose to plot the base peak chromatogram (BPC) to verify possible bad injections or outliers.

{{% /steps %}}
