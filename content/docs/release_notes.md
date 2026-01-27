---
title: "Patch Notes"
weight: 7
---

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
