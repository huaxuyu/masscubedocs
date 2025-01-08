---
linkTitle: "Data preparation"
title: "Data preparation"
weight: 1
---

## File conversion

Raw LC-MS data need to be converted to **mzML** or **mxXML** format for further processing in MassCube.

{{< callout type="warnings" >}}
Currently, only **centroid** data are supported in MassCube.
{{< /callout >}}

We recommend to use **MSConvert** for file conversion.

### Download and install MSConvert

Visit the [official website](https://proteowizard.sourceforge.io/download.html) to download ProteoWizard.

### File conversion using MSConvert

![](MSConvert.png "Fig. 1. MSConvert GUI")

{{% steps %}}

### Step 1. Set options

Check the boxes as shown in **Fig. 1**.

{{< callout type="warning" >}}
Do NOT check **Use Zlib compression**.
{{< /callout >}}

### Step 2. Set the Peak Picking filter

### Step 3. Add the Peak Picking filter

### Step 4. Browse and load files

### Step 5. Start conversion

By default, the converted files will be saved in the same directory as the raw files.

{{% /steps %}}

{{< details title="Convert files in command line mode" closed="true">}}
You can also convert files using MSConvert in command line mode. For more information, please refer to the [documentation](https://proteowizard.sourceforge.io/tools/msconvert.html).
{{< /details >}}

## Parameter file

A parameter file (.csv) is used to set parameters for the workflow. A templete is provided [here](https://github.com/huaxuyu/masscubedocs/blob/main/content/docs/parameters.csv). If not provided, the [default parameters](../parameters) will be applied. For MassCube version 1.0 or earlier, please use this [template](https://github.com/huaxuyu/masscubedocs/blob/main/content/docs/parameters_ver1.csv).

## Sample table

A sample table (.csv) is used to claim the name of samples and their groups including biological groups, quality control samples, or blank samples. A templete is provided [here](https://github.com/huaxuyu/masscubedocs/blob/main/content/docs/sample_table.csv). For MassCube version 1.0 or earlier, please use this [template](https://github.com/huaxuyu/masscubedocs/blob/main/content/docs/sample_table_ver1.csv)

For large-scale metabolomics data, it's not easy to prepare the sample table manually. In MassCube, we provide a function to automatically generate the sample table based on the file names in the data folder, and users can further define the groups.

### Automatically generate sample table

In the project folder, open a terminal and run the following command:

```bash
generate-sample-table
```

Your project folder should include a subfolder named **data** that contains the raw LC-MS data files in **mzML** or **mzXML** format.

```
my_project
├── data
│ ├── sample1.mzML
│ ├── sample2.mzML
| └── ...
|── ...
```

{{< callout type="warnings" >}}
You need to further edit the generated sample table to specify QCs, blanks and sample groups.
{{< /callout >}}
