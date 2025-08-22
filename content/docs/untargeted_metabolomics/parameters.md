---
linkTitle: "Set parameters"
title: Set parameters
weight: 3
---

[Download the default parameters](https://huaxuyu.github.io/masscube_parameters/). Make sure to check and adjust the following three key parameters:

{{% steps %}}

### ion_mode

Set to "positive" or "negative".

### ms1_abs_int_tol

You may use 30000 for Orbitrap data, and 1000 for TOF data.

### ms2_library_path

The absolute path to the MS/MS database file (e.g. D:/databases/ms2_library.mzML).

{{< /steps >}}

## Key parameters

Here we summarized six most important parameters in _masscube_ for untargeted metabolomics data processing:

1. **mz_tol_ms1**: the mass tolerance for MS1 feature detection. `0.005-0.01` Da is recommended.
2. **ms1_abs_int_tol**: the intensity tolerance for MS signals. `1000` is recommended for TOF data, and `30000` is recommended for Orbitrap data.
3. **mz_tol_alignment**: the mass tolerance for feature alignment. `0.01-0.015` Da is recommended.
4. **rt_tol_alignment**: the RT tolerance for feature alignment. `0.1-0.3` min is recommended.
5. **ms2_sim_tol**: the threshold for MS/MS similarity score. `0.7-0.8` is recommended.
6. **ms2_library_path**: the MS/MS library for MS/MS annotation.

## More about parameters

Explanation of the commonly used parameters for the `untargeted-metabolomics` workflow can be found [here](https://huaxuyu.github.io/masscube_parameters/).

For more tunable parameters, please refer to the [API documentation](/docs/api) or the source code in the `params` module.
