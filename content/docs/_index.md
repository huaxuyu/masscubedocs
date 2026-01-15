---
linkTitle: "Documentation"
title: MassCube Documentation
---

Hello! Welcome to the MassCube documentation!

**Date**: 2025-11-12 **Version**: 1.2.12

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

## Patch notes for v1.2.14

- Added precursor ion fraction (PIF) as an indicative metric for MS/MS spectrum quality. The PIF value is calculated based on isolation window and all ions present in the window that may contribute to the MS/MS spectrum. The PIF value is available in the aligned feature table in the "precursor_ion_fraction" column.

- Added precursor window as an attribute in the Scan object (Scan.isolation_window).

- Bug fix: now MassCube can correctly handle mzXML files without timestamps. Explanation: timestamps are automatically acquired in MassCube for signal drift normalization (if enabled). However, some mzXML files may not contain timestamps, which may lead to errors during data processing. This bug has been fixed in this version.

- Updated formula_to_isotope_distribution function.

- Minor text edits for the untargeted metabolomics workflow command line application.

Previous patch notes can be found [here](/docs/release_notes).
