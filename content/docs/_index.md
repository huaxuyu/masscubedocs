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

## Release Notes for v1.2.12

- Split the feature segmentation method into a standalone module.

- Re-optimized parameters for gf-prominence method (sigma = 0.6, prom_ratio = 0.02).

- Fixed overly long peak shape output in the aligned feature table.

- Updated formula_to_isotope_distribution function.

- Minor text and code edits.
