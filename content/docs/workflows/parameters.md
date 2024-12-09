---
linkTitle: "Parameters"
title: Parameters
weight: 2
---

Parameters are critical for MS data processing. However, setting parameters are often challenging, especially for beginners. _masscube_ provides a default parameter setting for users to start with.

The default parameters are optimized for most untargeted metabolomics studies. Users can also customize the parameters by providing a parameter file.

## Key parameters

Here we summarized six most important parameters in _masscube_ for untargeted metabolomics data processing:

1. **MS1 mass tolerance**: the mass tolerance for MS1 feature detection. `0.005-0.01` Da is recommended.
2. **Intensity tolerance**: the intensity tolerance for MS signals. `1000` is recommended for TOF data, and `30000` is recommended for Orbitrap data.
3. **Mass tolerance for alignement**: the mass tolerance for feature alignment. `0.01-0.015` Da is recommended.
4. **RT tolerance for alignment**: the RT tolerance for feature alignment. `0.1-0.3` min is recommended.
5. **MS/MS similarity score threshold**: the threshold for MS/MS similarity score. `0.7-0.8` is recommended.
6. **MS/MS library**: the MS/MS library for MS/MS annotation.

## Default parameters

_masscube_ automatically acquire the analytical metadata from the raw files including the mass spectrometer type and ionization mode. The corresponding default parameters will be applied based on the metadata.

## Customize parameters

From the [template](), users can customize the parameters by providing a parameter file. The parameter file should be a `.csv` file with the following columns:

| Parameter            | Value       | Explanation                                                                          |
| -------------------- | ----------- | ------------------------------------------------------------------------------------ |
| ion_mode             | positive    | MS ion mode, "positive" or "negative"                                                |
| ms_type              | qtof        | type of MS, "orbitrap", "qtof", "tripletof" or "others"                              |
| is_centroid          | yes         | whether the raw data is centroid data, "yes" or "no"                                 |
| mz_lower_limit       | 0           | lower limit of m/z in Da                                                             |
| mz_upper_limit       | 100000      | upper limit of m/z in Da                                                             |
| rt_lower_limit       | 0           | lower limit of retention time in minutes                                             |
| rt_upper_limit       | 10000       | upper limit of retention time in minutes                                             |
| ms1_abs_int_tol      | 1000        | absolute intensity threshold for MS1, recommend 30000 for Orbitrap and 1000 for QTOF |
| ms2_abs_int_tol      | 500         | absolute intensity threshold for MS2, recommend 10000 for Orbitrap and 500 for QTOF  |
| mz_tol_ms1           | 0.01        | m/z tolerance for MS1, default is 0.01                                               |
| mz_tol_ms2           | 0.015       | m/z tolerance for MS2, default is 0.015                                              |
| scan_scan_cor_tol    | 0.7         | scan-to-scan correlation tolerance for feature grouping, default is 0.7              |
| mz_tol_alignment     | 0.01        | m/z tolerance for alignment, default is 0.01                                         |
| rt_tol_alignment     | 0.2         | RT tolerance for alignment, default is 0.2                                           |
| correct_rt           | yes         | whether to perform RT correction                                                     |
| merge_features       | yes         | whether to clean feature table by merging features with almost the same m/z and RT   |
| ms2_library_path     |             | path to the MS2 library (.msp or .pickle)                                            |
| ms2_sim_tol          | 0.7         | MS2 similarity tolerance                                                             |
| fuzzy_search         | yes         | whether to perform fuzzy search                                                      |
| sample_normalization | no          | whether to normalize the data based on total sample amount/concentration             |
| signal_normalization | no          | whether to run feature-wised normalization to correct systematic signal drift        |
| run_statistics       | no          | whether to perform statistical analysis                                              |
| plot_bpc             | yes         | whether to plot base peak chromatograms                                              |
| plot_ms2             | yes         | whether to plot mirror plots for MS2 matching                                        |
| quant_method         | peak_height | value for quantification and output, "peak_height", "peak_area" or "top_average"     |
| by_group_name        |             | group name for classification                                                        |

## More about parameters

Almost all parameters in _masscube_ are tunable to ensure flexibility and adaptability for different datasets. For programmers, please refer to each function and object in the [API documentation](/docs/api/) for more details.
