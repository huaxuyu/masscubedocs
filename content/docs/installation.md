---
title: "Installation"
weight: 1
---

## Install Python

Visit the [official Python website](https://www.python.org/) to download Python. **Python 3.9-3.11** is recommended.

{{% details title="Download Python 3.11.7" closed="true" %}}
Download [Python 3.11.7](https://www.python.org/downloads/release/python-3117/).
{{% /details %}}

**IMPORTANT**: Make sure to check the box that says "Add Python to PATH" during installation.

## Install _masscube_

_masscube_ is a Python package that can be installed using **pip**. Open terminal and run

```console
pip install masscube
```

To update the package to the latest version, open terminal and run

```console
pip install masscube --upgrade
```

Dependencies will be automatically installed. Consider creating a [virtual environment](https://docs.python.org/3/library/venv.html) if you're working with Python on multiple projects.

{{% details title="Dependencies" closed="true"%}}

```
dependencies = [
    "numpy>=1.24",
    "pandas>=2.2.1",
    "pyteomics==4.6.3",
    "scipy>=1.10.1",
    "tqdm>=4.66.1",
    "lxml>=4.9.3",
    "matplotlib>=3.8.2",
    "ms_entropy==1.2.2",
    "scikit-learn>=1.3.2",
    "statsmodels>=0.14.2",
    "umap-learn>=0.5.7",
]
```

{{% /details %}}
