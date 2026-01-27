---
linkTitle: "Documentation"
title: MassCube Documentation
---

Hello! Welcome to the MassCube documentation!

**Date**: 2026-01-26 **Version**: 1.2.15

<!--more-->

## What is MassCube?

MassCube is a Python computing library for mass spectrometry data processing in metabolomics.

## Features

- **Open-source**: Free for non-commercial use.

- **Workflows**: Complete the entire data processing pipeline with a single command.

- **Accurate**: Efficient large-scale data processing with human-expert level accuracy.

- **Modules**: 16 modules to cover the whole workflow.

## Getting Started

{{< cards >}}
{{< card link="../docs/installation" title="Installation" icon="play">}}
{{< card link="../docs/quickstart" title="Quick Start" icon="play">}}
{{< /cards >}}

## Must reads

- Starting from MassCube ver. 1.2.8, only one database is needed for the untargeted metabolomics workflow. Make sure you [download the latest version of MS/MS database](https://zenodo.org/records/17902514).

## Patch notes for v1.2.15

- Scan-to-scan correlation values are now reported for annotated adducts and in-source fragments.
- Isotope state is clearly specified in the feature table (e.g. M+2 instead of “isotope”)
- Isotope recognition accuracy has been improved for high-resolution MS data: C and S isotopes can be better distinguished
- Feature grouping speed is now improved by 10-fold
- Bug fix: mzXML file may not correctly specify the isolation window for DDA, which can trigger an error for precursor ion fraction calculation
- Bug fix: in very rare cases, feature segmentation may fail
- Feature alignment speed is improved.
- Scan index (the index of the MS/MS scan in the raw reference file) is now provided for the MS/MS spectrum in the feature table that is used for annotation.

Previous patch notes can be found [here](../release_notes).
