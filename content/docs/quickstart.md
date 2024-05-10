---
title: "Quick Start"
weight: 2
---

Let's get started with the OneClick Untargeted Metabolomics workflow. This page will show you how to process your data with a single line of command. 

If you haven't installed MassCube, please follow the [installation guide](../installation).

## The OneClick Untargeted Metabolomics workflow

The OneClick workflow is designed make the untargeted metabolomics analysis easier. It integrates metadata curation, feature detection, evaluation, alignment, annotation, signal correction, and statistical analysis (**Fig. 1**).

![](untargeted_workflow.png "Fig. 1. The OneClick Untargeted Metabolomics workflow")

### Input

In your project folder (e.g. **my_project**), you need to prepare the following files and folders:

```
my_project
├── data
│   ├── sample1.mzML
│   ├── sample2.mzML
|   └── ...
|── sample_table.csv
└── parameters.csv
```

There are three components for a project:

1. `data` folder: a file folder containing all raw LC-MS data in .mzML or .mzXML format. It's **mandatory**.
2. `sample_table.csv` file: a csv file to claim the name of samples and their groups including biological groups, quality control samples, or blank samples. A template is [here](). It's **optional**. If not provided, normalization and statistical analysis will not be applied.

{{< callout type="warning" >}}
  In sample table, please name quality control samples as "qc" and blank samples as "blank" (not case-sensitive).
{{< /callout >}}

3. `parameters.csv` file: a csv file to set parameters for the workflow. A template is [here](). It's **optional**. If not provided, the [default parameters](../docs/parameter) will be applied, yet **MS/MS annotation will not be performed since the library directory is not provided**.



More about the data preparation:

{{< cards >}}
  {{< card link="../data_preparation" title="Data Preparation" icon="play">}}
{{< /cards >}}


### Processing

In the project folder, open a terminal and run the following command:

```bash
untargeted-metabolomics
```

{{< callout type="warning" >}}
  Make sure the terminal directory is the project folder. For [Windows user](https://johnwargo.com/posts/2024/launch-windows-terminal/) and [MacOS user](https://support.apple.com/guide/terminal/open-or-quit-terminal-apd5265185d-f365-44cb-8b09-71a064a42125/mac#:~:text=Terminal%20for%20me-,Open%20Terminal,%2C%20then%20double%2Dclick%20Terminal.)
{{< /callout >}}

### Output

After the processing, you will find the following files and folders in the project folder:

```
project/
├── data
├── sample_table.csv
├── parameters.csv
├── project.mc
├── aligned_feature_table.csv
├── single_file_output
│   ├── sample1.csv
│   ├── sample2.csv
│   └── ...
├── chromatogram
│   ├── sample1.png
│   ├── sample2.png
│   └── ...
├── ms2_matching
│   ├── compound1.png
│   ├── compound2.png
│   └── ...
├── statistics
├── ...
```

1. `project.mc` file: the project file of *masscube*.
2. `aligned_feature_table.csv` file: feature table after alignment.
3. `single_file_output` folder: a file folder containing the detected features from individual files.
4.  `chromatogram` folder: a file folder to store base peak chromatograms (BPCs) for individual files.
5. `ms2_matching` folder: mirror plot of MS2 matching results.
6. `statistics` folder: results from statistical analysis like principal component analysis (PCA).