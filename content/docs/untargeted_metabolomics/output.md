---
linkTitle: "About the output"
title: "Explanation of output files"
weight: 6
---

After processing, MassCube generates output files in the project folder as described below.

```
my_project/
├── data
├── sample_table.csv
├── parameters.csv
├── mzrt_list.csv
├── aligned_feature_table.txt
├── normalized_feature_table.txt
├── project_files
│   ├── features.msp
│   ├── aligned_feature_table_before_annotation.txt

│   └── ...
├── single_files
│   ├── sample1.txt
│   ├── sample2.txt
│   └── ...
├── chromatograms
│   ├── sample1.png
│   ├── sample2.png
│   └── ...
├── ms2_matching
│   ├── compound1.png
│   ├── compound2.png
│   └── ...
├── statistical_analysis
├── normalization_results
│   ├── feature_1_normalization.png
│   ├── feature_2_normalization.png
│   └── ...
├── ...
```

## aligned_feature_table.txt

Samples are in columns, and features are in rows. From left to right, the columns are:

- group_ID: the ID of the feature group. Features with the same group_ID are considered to originate from the same neutral compound (i.e., isotopes, adducts, and in-source fragments are grouped together).
- feature_ID: the ID of features ranked by maximum intensity from high to low.
- m/z: mass-to-charge ratio.
- RT: retention time in minutes.
- adduct: the adduct type.
- is_isotope: whether the feature is an isotope (TRUE or FALSE).
- is_in_source_fragment: whether the feature is an in-source fragment (TRUE or FALSE).
- Gaussian_similarity: the similarity score (0–1) that measures how well the ion trace fits a Gaussian curve.
- noise_score: the score (0–∞) that measures the level of noise. A noise score > 0.5 indicates considerable noise.
- asymmetry_factor: the asymmetry factor of the peak.
- peak_shape: the retention time–intensity pairs of the peak shape: RT1;intensity1 | RT2;intensity2 | ...
- detection_rate: the fraction of non-blank files in which the feature was detected.
- detection_rate_gap_filled: after gap filling, the fraction of non-blank files in which the feature was detected.
- alignment_reference_file: the reference file for alignment. It also provides the peak shape information.
- charge: the number of charges.
- isotopes: isotope distribution acquired from the alignment reference file: mz1;intensity1 | mz2;intensity2 | ...
- MS2_reference_file: the source file of the MS/MS spectrum.
- MS2: the experimental MS/MS spectrum.
- matched_MS2: the database MS/MS spectrum.
- search_mode: identity_search, fuzzy_search, or mzRT_match.
- annotation: the compound name.
- formula: the molecular formula.
- similarity: the similarity score (0–1) between the experimental and database MS/MS spectra.
- matched_peak_number: the number of matched peaks.
- SMILES: the SMILES representation of the compound.
- InChIKey: the InChIKey representation of the compound.

If normalization is performed, the corresponding "normalized_feature_table.txt" file and "normalization_results" folder will be provided.

## project_files

A folder that contains the project files including

- features.msp: a MSP file containing all detected features for further analyses.
- aligned_feature_table_before_annotation.txt: the unannotated feature table.
- aligned_features.pkl: a pickle file containing the aligned features as a list.

## single_files

A folder that contains txt files for each raw MS data after feature detection and segmentation.

## chromatograms

A folder that contains base peak chromatograms for each raw MS data.

## ms2_matching

A folder that contains mirror plots of MS/MS spectral matching results. Only identity search annotations will be plotted.
