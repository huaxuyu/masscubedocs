---
title: "Patch Notes"
weight: 7
---

## Patch notes for v1.2.15

- Scan-to-scan correlation values are now reported for annotated adducts and in-source fragments.
- Isotope state is clearly specified in the feature table (e.g. M+2 instead of “isotope”)
- Isotope recognition accuracy has been improved for high-resolution MS data: C and S isotopes can be better distinguished
- Feature grouping speed is now improved by 10-fold
- Bug fix: mzXML file may not correctly specify the isolation window for DDA, which can trigger an error for precursor ion fraction calculation
- Bug fix: in very rare cases, feature segmentation may fail
- Feature alignment speed is improved.
- Scan index (the index of the MS/MS scan in the raw reference file) is now provided for the MS/MS spectrum in the feature table that is used for annotation.

## Patch notes for v1.2.14

- Added precursor ion fraction (PIF) as an indicative metric for MS/MS spectrum quality. The PIF value is calculated based on isolation window and all ions present in the window that may contribute to the MS/MS spectrum. The PIF value is available in the aligned feature table in the "precursor_ion_fraction" column.

- Added precursor window as an attribute in the Scan object (Scan.isolation_window).

- Bug fix: now MassCube can correctly handle mzXML files without timestamps. Explanation: timestamps are automatically acquired in MassCube for signal drift normalization (if enabled). However, some mzXML files may not contain timestamps, which may lead to errors during data processing. This bug has been fixed in this version.

- Updated formula_to_isotope_distribution function.

- Minor text edits for the untargeted metabolomics workflow command line application.

## v1.2.13

- Fixed a bug that may cause failed MS/MS parsing.

## v1.2.12

- Split the feature segmentation method into a standalone module.

- Re-optimized parameters for gf-prominence method (sigma = 0.6, prom_ratio = 0.02).

- Fixed overly long peak shape output in the aligned feature table.

- Updated formula_to_isotope_distribution function.

- Minor text and code edits.
