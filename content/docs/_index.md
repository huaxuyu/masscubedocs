---
linkTitle: "Documentation"
title: MassCube Documentation
---

Hello! Welcome to the MassCube documentation!

**Date**: 2025-05-31 **Version**: 1.2.5

<!--more-->

## What is MassCube?

MassCube is an open-source computing library and framework for MS data processing in Python. It supports comprehensive functionalities and workflows designed for versatile data processing tasks.

## Features

- **Open-source**: Free for non-commercial use.

- **Modular design**: Easily extendable functionalities.

- **User-friendly**: Command-line interface for easy data processing.

- **Scalable**: Efficient and memory-friendly handling of large-scale metabolomics data.

- **Reproducible**: Metadata tracking for recording parameters, dependencies, and module order.

- **Visualization**: Tools for intuitive data exploration and publication-quality figure creation.

## Getting Started

{{< cards >}}
{{< card link="../docs/installation" title="Installation" icon="play">}}
{{< card link="../docs/quickstart" title="Quick Start" icon="play">}}
{{< /cards >}}

## Release Notes for v1.2

- MassCube now annoatate MS/MS spectra using unweighted entropy similarity based on the ms_entropy Python package ver. 1.3.4. Please make sure you use the latest version of the MS/MS library. Check quick start for more details.

- Now you can plot signal normalization results by setting plot_normalization to True in the parameters.csv file.

- Bug fixes and performance improvements.
