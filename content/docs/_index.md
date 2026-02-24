---
linkTitle: "Documentation"
title: MassCube Documentation
---

Hello! Welcome to the MassCube documentation!

**Date**: 2026-02-23 **Version**: 1.2.16

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

## Patch notes for v1.2.16

- Bug fix: now the scan number and precursor ion fraction values are correctly assigned based on the reference MS/MS spectrum (i.e. the spectrum used for annotation)
- Empty adduct is now allowed for calculating the isotope distribution.
- Other minor changes of code notes.

Previous patch notes can be found [here](../docs/release_notes).
