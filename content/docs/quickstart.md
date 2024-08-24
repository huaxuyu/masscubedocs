---
linkTitle: "Quick start"
title: "Quick Start"
weight: 2
---

Let's get started with the **OneClick** untargeted metabolomics workflow. This workflow is designed to streamline untargeted metabolomics analysis, providing comprehensive results with a single command.

If you haven't installed MassCube, please follow the [installation guide](../installation).

## The OneClick untargeted metabolomics workflow

Metabolomics data processing could be challenging for researchers. The OneClick untargeted metabolomics workflow was developed to address the burdens and support metabolomics research.

The OneClick workflow integrates metadata curation, feature detection, evaluation, alignment, annotation, and statistical analysis to provide users with a comprehensive view of the data (**Fig. 1**).

![](untargeted_workflow.png "Fig. 1. The OneClick untargeted metabolomics workflow")

{{% steps %}}

### Input (3+1)

You need <u>three components</u> for the project plus <u>one MS/MS library</u> for annotation.

In your project folder (e.g. **my_project**), you need to prepare the following components:

```
my_project
├── data
│   ├── sample1.mzML
│   ├── sample2.mzML
|   └── ...
|── sample_table.csv
└── parameters.csv
```

1. `data` folder: a file folder containing all raw LC-MS data in <u>.mzML</u> or <u>.mzXML</u> format. It's **mandatory**. Instructions for file conversion are provided [here](../workflows/data_preparation).

2. `sample_table.csv` file: a csv file to claim the sample groups including biological groups, quality control samples, or blank samples. A template can be downloaded from [here](https://github.com/huaxuyu/masscubedocs/blob/main/content/docs/sample_table.csv). It's **optional**. If not provided, normalization and statistical analysis will not be applied. **Note:** In sample table, please name quality control samples as "qc" and blank samples as "blank" (not case-sensitive).

3. `parameters.csv` file: a csv file to set parameters for the workflow. A template can be downloaded from [here](https://github.com/huaxuyu/masscubedocs/blob/main/content/docs/parameters.csv). It's **optional**. If not provided, the [default parameters](../parameter) will be applied, yet **annotation will not be performed since the MS/MS library is not provided**.

4. **MS2 database**: To annotate MS/MS spectra, you need to download a MS/MS library from [here](https://zenodo.org/records/11363475). For faster database loading, please download and use the .pkl format.

**Extra component for annotation:**

1. `mzrt_list.csv` file: a csv file to provide the m/z and retention time for feature annotation. It was designed to annotate full-scan MS data or annotate the spiked internal standards. A template can be downloaded from [here](https://github.com/huaxuyu/masscubedocs/blob/main/content/docs/mzrt_list.csv). It's **optional**. If not provided, the annotation will not be performed.

{{< cards >}}
{{< card link="../workflows/data_preparation" title="Data Preparation" icon="play">}}
{{< /cards >}}

### Processing

**In the project folder**, open a terminal and run the following command:

```bash
untargeted-metabolomics
```

{{< details title="How to open the terminal" closed="true" >}}
Make sure the terminal directory is set to the project folder. For [Windows user](https://johnwargo.com/posts/2024/launch-windows-terminal/) and [MacOS user](https://support.apple.com/guide/terminal/open-or-quit-terminal-apd5265185d-f365-44cb-8b09-71a064a42125/mac#:~:text=Terminal%20for%20me-,Open%20Terminal,%2C%20then%20double%2Dclick%20Terminal.)
{{< /details >}}

### Output

After the processing, you will find the following files and folders in the project folder:

```
project/
├── data
├── sample_table.csv
├── parameters.csv
├── project.mc
├── aligned_feature_table.txt
├── aligned_feature_table_before_normalization.txt
├── ms2.msp
├── single_file_output
│   ├── sample1.txt
│   ├── sample2.txt
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

1. `project.mc` file: the project file of _masscube_.
2. `aligned_feature_table.csv` file: feature table after alignment (if applied).
3. `aligned_feature_table_before_normalization.csv` file: feature table before normalization.
4. `ms2.msp` file: MS/MS spectra for detected features that can be further analyzed on other platforms.
5. `single_file_output` folder: a folder containing the feature table for each sample.
6. `chromatogram` folder: a folder containing the chromatogram for each sample.
7. `ms2_matching` folder: a folder containing the MS/MS matching for each annotated compound.
8. `statistics` folder: a folder containing the statistical analysis results.

{{% /steps %}}
