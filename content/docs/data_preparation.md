---
linkTitle: "Data preparation"
title: "Data preparation"
weight: 3
---

## File conversion

Raw LC-MS data need to be converted to **mzML** or **mxXML** format. We recommend to use **ProteoWizard**
for file conversion.

### Download and install ProteoWizard

Visit the [official website](https://proteowizard.sourceforge.io/download.html) to download ProteoWizard.

### File conversion using MSConvert

![](MSConvert.png "Fig. 1. MSConvert GUI")

* **Step 1. Set options**

Check the boxes as shown in **Fig. 1**.

{{< callout type="warning" >}}
   Do NOT check **Use Zlib compression**.
{{< /callout >}}

* **Step 2. Set the Peak Picking filter**

* **Step 3. Add the Peak Picking filter**

* **Step 4. Browse and load files**

* **Step 5. Start conversion**

By default, the converted files will be saved in the same directory as the raw files.

{{< callout type="info" >}}
   You can also convert files using MSConvert in command line mode. For more information, please refer to the [documentation](https://proteowizard.sourceforge.io/tools/msconvert.html).
{{< /callout >}}


## Sample table

Sample table 



## Parameter file