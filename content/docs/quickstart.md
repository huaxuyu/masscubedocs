---
title: "Quick Start"
weight: 1
---

Let's get started with the OneClick Untargeted Metabolomics workflow. This page will show you how to process your data with a single line of command. 


## The OneClick Untargeted Metabolomics workflow

The OneClick workflow is designed make the untargeted metabolomics analysis easier. It integrates metadata curation, feature detection, evaluation, alignment, annotation, signal correction, and statistical analysis (**Fig. 1**).

![](workflow.png "Fig. 1. The OneClick Untargeted Metabolomics workflow")

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
2. `sample_table.csv` file: a csv file to claim the name of samples and their groups including biological groups, quality control samples, or blank samples. An example is [here](). It's **mandatory**.
3. `parameters.csv` file: a csv file to set parameters for the workflow. An example is [here](). It's **optional**. If not provided, the [default parameters]() will be applied, yet MS/MS annotation will not be performed since the library directory is not provided. See [Parameters]() for more details. 

{{< cards >}}
  {{< card link="../data_preparation" title="Data Preparation" icon="play">}}
{{< /cards >}}


### Processing

Within the project folder, open terminal and run

```
untargeted-metabolomics
```

{{< callout type="warning" >}}
  Make sure the terminal directory is the project folder. For [Windows user](https://johnwargo.com/posts/2024/launch-windows-terminal/) and [MacOS user](https://support.apple.com/guide/terminal/open-new-terminal-windows-and-tabs-trmlb20c7888/mac#:~:text=Open%20new%20Terminal%20windows%20or%20tabs%20from%20the%20Finder&text=Control%2Dclick%20the%20folder%20in,New%20Terminal%20Tab%20at%20Folder.)
{{< /callout >}}

### Output

A set of output files will be provided in the **project folder** depending on the parameters settings. The general output will be

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
6. `statistics` folder: results from statistical analysis. For example, principal component analysis plots.