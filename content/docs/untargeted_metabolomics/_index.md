---
linkTitle: "Untargeted metabolomics"
title: Untargeted metabolomics
weight: 3
---

This is a complete data processing workflow for untargeted metabolomics.

The workflow consists of the following steps:

1. **Raw data reading**: Import raw MS data files in mzML or mzXML format.

2. **Feature detection**: Detect peaks in the raw MS data.

3. **Feature segmentation**: Resolve partially overlapping peaks for isomer recognition.

4. **Feature grouping**: Group isotopes, adducts, and in-source fragments.

5. **Feature alignment**: Align detected features across multiple samples to account for m/z and retention time variations.

6. **Feature annotation**: Conventional identity search and advanced fuzzy search.

7. **Statistical analysis**: Compare sample groups.
