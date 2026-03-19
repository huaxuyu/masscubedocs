---
linkTitle: "Documentation"
title: MassCube Documentation
---

Hello! Welcome to the MassCube documentation!

**Date**: 2026-03-19 **Version**: 1.2.19

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

## Patch notes for v1.2.19

- Improved the alignment accuracy by optimizing the alignment strategy. RT and m/z errors were considered together for better alignment results.
- The finally reported m/z value for aligned feature is now the median m/z value across all samples instead of the m/z value in the reference sample.
- Upper limits for mz_tol_ms1 and mz_tol_ms2 were set to 5.0 Da (0.02 Da before) for low-resolution MS data.
- Code updates for database loading.
- Default centroid_mz_tol (i.e. MS1 ions with m/z difference lower than this value will be combined before processing, designed for bad data deconvolution from Orbitrap MS) is changed from 5 mDa to 2 mDa.
- Other minor changes of code notes.
- New safe float function for better raw data loading.
- Better indicators for error handling in the workflow.

Previous patch notes can be found [here](../docs/release_notes).
