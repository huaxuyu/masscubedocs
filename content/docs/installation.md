---
title: "Installation"
weight: 1
---


## Install Python

Visit the [official Python website](https://www.python.org/) to download Python.

{{% details title="Download Python 3.11" closed="true" %}}
   **Python 3.9-3.11** is recommended. Download [Python 3.11](https://www.python.org/downloads/release/python-3117/).
{{% /details %}}

## Install *masscube*

*masscube* is a Python package that can be installed using **pip**. Open terminal and run

```console
pip install masscube
```

Dependencies will be automatically installed. Consider creating a [virtual environment](https://docs.python.org/3/library/venv.html) if you're working with Python on multiple projects.

{{% details title="Dependencies" closed="true"%}}

```
"numpy>=1.24",
"pandas>=2.0",
"pyteomics>=4.6",
"scipy>=1.10.1",
"tqdm>=4.65.0",
"lxml>=4.9.2",
"matplotlib",
"ms_entropy>=1.1.1",
"networkx",
"scikit-learn"
```

{{% /details %}}