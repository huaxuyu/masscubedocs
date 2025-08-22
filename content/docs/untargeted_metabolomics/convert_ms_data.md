---
linkTitle: "Convert raw MS data"
title: "Convert raw MS data"
weight: 1
---

Raw mass spectrometry data need to be converted to <u>centroid</u> **mzML** or **mxXML** format for MassCube data processing.

We recommend to use **MSConvert** for file conversion.

Visit the [official website](https://proteowizard.sourceforge.io/download.html) to download ProteoWizard and install MSConvert.

![](MSConvert.png "Fig. 1. MSConvert GUI")

{{% steps %}}

#### Step 1. Set options

Check the boxes as shown in **Fig. 1**.

{{< callout type="warning" >}}
Do NOT check **Use zlib compression**.
{{< /callout >}}

#### Step 2. Set the peak picking filter

#### Step 3. Add the peak picking filter

#### Step 4. Browse and load files

#### Step 5. Start conversion

{{< /steps >}}

By default, the converted files will be saved in the same directory as the raw files.
