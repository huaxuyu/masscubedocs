---
linkTitle: "Parameters"
title: Parameters
weight: 2
---

`masscube` provides default parameters for users to start with. [Download the default parameters](https://huaxuyu.github.io/masscube_parameters/). You only need to change two settings based on your data:

{{% steps %}}

### ion_mode

"positive" or "negative"

### ms1_abs_int_tol

30000 for Orbitrap data, and 1000 for TOF data.

### ms2_library_path

absolute path to the MS/MS database file (e.g. D:/databases/ms2_library.mzML)

{{< /steps >}}

## Key parameters

Here we summarized six most important parameters in _masscube_ for untargeted metabolomics data processing:

1. **MS1 mass tolerance**: the mass tolerance for MS1 feature detection. `0.005-0.01` Da is recommended.
2. **Intensity tolerance**: the intensity tolerance for MS signals. `1000` is recommended for TOF data, and `30000` is recommended for Orbitrap data.
3. **Mass tolerance for alignement**: the mass tolerance for feature alignment. `0.01-0.015` Da is recommended.
4. **RT tolerance for alignment**: the RT tolerance for feature alignment. `0.1-0.3` min is recommended.
5. **MS/MS similarity score threshold**: the threshold for MS/MS similarity score. `0.7-0.8` is recommended.
6. **MS/MS library**: the MS/MS library for MS/MS annotation.

## More about parameters

For advanced programming users, much more parameters in `masscube` are tunable. Please refer to the [API documentation](/docs/api) for more details.
