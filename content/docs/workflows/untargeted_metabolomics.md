---
linkTitle: "Untargeted metabolomics"
title: Untargeted metabolomics workflow
weight: 4
---

## Introduction

Data processing is critical for metabolomics studies. A series of steps are required to process the raw data to generate biological hypothesis that can be further validated.

The MassCube untargeted metabolomics workflow aims to address the burdens in mass spectrometry-based metabolomics data processing. It integrates metadata curation, feature detection, evaluation, alignment, annotation, and statistical analysis to provide users with a comprehensive view of the data.

## How to use

Please refer to the [quick start guide](/docs/quickstart).

## Explainations of the workflow

```python {linenos=table,hl_lines=[],linenostar=1}
def untargeted_metabolomics_workflow(path=None, return_results=False, only_process_single_files=False, return_params_only=False):
    """
    The untargeted metabolomics workflow. See the documentation for details.

    Parameters
    ----------
    path : str
        The working directory. If None, the current working directory is used.
    return_results : bool
        Whether to return the results. Default is False.
    only_process_single_files : bool
        Whether to only process the single files. Default is False.
    return_params_only : bool
        Whether to return the parameters only. Default is False.

    Returns
    -------
    features : list
        A list of features.
    params : Params object
        Parameters for the workflow.
    """
    ...
```

{{% steps %}}

### Step 1. Define or load parameters

Parameters are critical for MS data processing. However, setting parameters are often challenging, especially for beginners or scientists who are not familiar with the MS data.

_masscube_ automatically read the MS data and apply the corresponding default parameters. Users can also customize the parameters by providing a parameter file.

### Step 2. Load sample table and organize data

A sample table is used to claim the name of samples and their groups. In most metabolomics studies, quality control samples and blank samples are included. _masscube_ automatically apply normalization and statistical analysis if the sample table is provided.

### Step 3. Single file processing

Individual files are processed for feature detection, which envolves the detection of peak apex, edges, area, and related MS/MS spectra. By default, features are not grouped in this step to reduce computational cost, and grouping will be performed in the alignment step.

To accelerate the processing, _masscube_ supports parallel computing for multiple files. By default, the number of threads is set to be the 80% of the total CPU cores so that the computer can still be used for other tasks.

To control the memory usage, the files are processed in batches. The default batch size is 100.

### Step 4. Feature alignment

Feature alignment aims to match the same feature across different samples. The alignment is based on the mass-to-charge ratio and retention time. The mass tolerance and retention time tolerance are critical for the alignment. It also includes the annotation of isotopes, charge states, adducts, and in-source fragments.

### Step 5. Gap filling

Gap filling is critical for the downstream statistical analysis, and missing values are treated by forced peak detection.

### Step 6. MS/MS annotation

Compound annotation was performed by matching the experimental MS/MS spectra with the MS/MS library. The MS/MS similarity score is generated to indicate the confidence of the annotation.

Flash entropy search is used to accelerate the annotation. _masscube_ also provides analog search (i.e. hybrid search) for unknown discovery.

### Step 7. Normalization

Two types of normalization could be needed in metabolomics to address the systematic signal drifts and the sample-to-sample variation (i.e. total amount/concentration difference). _masscube_ provides multiple post-acquisition normalization algorithms to address the normalization issue.

### Step 8. Statistical analysis

Univariate and multivariate statistical analysis will be performed if sample table is provided. The results will be saved in the `statistics` folder.

### Step 9. Data visualization

Users can choose to plot the base peak chromatogram (BPC) to verify possible bad injections or outliers. The MS/MS matching plots are generated for the annotated compounds. PCA plots are generated for the statistical analysis.

{{% /steps %}}
