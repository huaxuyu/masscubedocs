---
linkTitle: "Parameters"
title: Parameters
weight: 2
---

Parameters are critical for MS data processing. However, setting parameters are often challenging, especially for beginners. *masscube* provides a default parameter setting for users to start with. 

The default parameters are optimized for most untargeted metabolomics studies. Users can also customize the parameters by providing a parameter file.

## Key parameters

Here we summarized six most important parameters in *masscube* for untargeted metabolomics data processing:

1. **MS1 mass tolerance**: the mass tolerance for MS1 feature detection. `0.005-0.01` Da is recommended.
2. **Intensity tolerance**: the intensity tolerance for MS signals. `1000` is recommended for TOF data, and `30000` is recommended for Orbitrap data.
3. **Mass tolerance for alignement**: the mass tolerance for feature alignment. `0.01-0.015` Da is recommended.
4. **RT tolerance for alignment**: the RT tolerance for feature alignment. `0.1-0.3` min is recommended.
5. **MS/MS similarity score threshold**: the threshold for MS/MS similarity score. `0.7-0.8` is recommended.
6. **MS/MS library**: the MS/MS library for MS/MS annotation.


## Default parameters

*masscube* automatically acquire the analytical metadata from the raw files including the mass spectrometer type and ionization mode. The corresponding default parameters will be applied based on the metadata.


## Customize parameters

From the [template](), users can customize the parameters by providing a parameter file. The parameter file should be a `.csv` file with the following columns:

| Parameter| Value | Explanation
| --------  | -------- | ------ |
| rt_start | 0 | start of the analytical gradient; minute
| rt_end | 23 | end of the analytical gradient; minute
| ion_mode | negative | "positive" or "negative"
| mz_tol_ms1 | 0.01 | m/z tolerance for MS1 spectra; Da
| mz_tol_ms2 | 0.015 | m/z tolerance for MS2 spectra; Da
| int_tol | 1000 | Intensity tolerance; 1000 for TOF and 30000 for orbitrap
| align_mz_tol | 0.01 | m/z tolerance for alignment; Da
| align_rt_tol | 0.2 | retention time tolerance for alignment; minute
| msms_library | | path to the MS2 library; msp or pickle
| ms2_sim_tol | 0.7 | MS2 similarity tolerance
| run_normalization | TRUE | TRUE or FALSE; whether to run post-acquisition sample normalization
| normalization_method | pqn | sample normalization algorithm
| plot_bpc | FALSE | TRUE or FALSE; whether to plot base peak chromatogram for individual files
| plot_ms2 | TRUE | TRUE or FALSE; whether to plot mirror plots for MS2 matching
| run_statistics | TRUE	| TRUE or FALSE; whether to run statistical analysis


## More about parameters

Almost all parameters in *masscube* are tunable to ensure flexibility and adaptability for different datasets. For programmers, please refer to each function and object in the [API documentation](/docs/api/) for more details.