---
linkTitle: "Database"
title: "Prepare a database"
weight: 3
---

## Introduction

A database is a collection of m/z, MS2 spectra, retentiont time, collision cross section, and other information of known compounds. It is used to identify the compounds in the LC-MS data. In this workflow, we introduce how to prepare a database for _masscube_.

## Download a database

For users without programming experience or just want to use a database directly, you can download a database from the [here](https://zenodo.org/records/11363475). For faster database loading, please download and use the .pkl format.

## Prepare a database (for advanced users)

Three formats are supported for the database: pickle, msp, and json. The pickle format is recommended for faster loading. The msp format is recommended for compatibility with other software. The json format is another human-readable format commonly used in Python.

### MSP format

An MSP database is a text file that contains the MS2 database. Each block contains the information of a compound. IMPORTANT: make sure the keys are consistent with the example below.

```text
NAME: L-PHENYLALANINE
PRECURSORMZ: 166.086013793945
PRECURSORTYPE: [M+H]+
IONMODE: Positive
RETENTIONTIME: 3.30520009994507
CCS: 136.819671630859
FORMULA: C9H11NO2
ONTOLOGY: Phenylalanine and derivatives
SMILES: C1=CC=C(C=C1)C[C@@H](C(=O)O)N
INCHIKEY: COLNVLDHVKWLRT-QMMMGPOBSA-N
INSTRUMENTTYPE: LC-ESI-QFT
COLLISIONENERGY: 35.0 eV
COMMENT: DB#=EMBL-MCF_spec98214; origin=EMBL - Metabolomics Core Facility Spectral Library
Num Peaks: 7
103.054	15
107.049	14
120.081	1000
121.084	16
131.049	41
149.059	16
166.086	56
```

Here, NAME, PRECURSORMZ and PRECURSORTYPE is mandatory. In particular,

1. if RETENTIONTIME is not provided, level 1 annotation (i.e. retention time and MS2 matching) will not be performed.
2. if any of FORMULA, SMILES or INCHIKEY is not provided, they will be missing in the output.
3. if MS2 spectra (lines below Num Peaks) are not provided but retention time is provided, mzrt matching will be performed. In this case, no similarity score will be calculated. But you can compare the experimental and matched retention time to see if they are close.

### Pickle format

A .pkl database is a FlashEntropySearch object that contains the MS2 database. ms_entropy version 1.2.2 is highly recommended to generate this object (other versions may not work). Here is an example of how to generate a .pkl database from a msp file:

```python
from masscube.annotation import index_msp_to_pkl

# it will output a database.pkl file in the same folder
index_msp_to_pkl('database.msp')
```

Check the source code of `index_.msp_to_pkl` for more details.

### JSON format

A JSON database is a list of dictionaries, each dictionary contains

```json
{
  "name": "L-PHENYLALANINE",
  "precursor_mz": 166.086013793945,
  "precursor_type": "[M+H]+",
  "ionmode": "Positive",
  "retentiontime": "3.30520009994507",
  "ccs": "136.819671630859",
  "formula": "C9H11NO2",
  "ontology": "Phenylalanine and derivatives",
  "smiles": "C1=CC=C(C=C1)C[C@@H](C(=O)O)N",
  "inchikey": "COLNVLDHVKWLRT-QMMMGPOBSA-N",
  "instrumenttype": "LC-ESI-QFT",
  "collisionenergy": "35.0 eV",
  "comment": "DB#=EMBL-MCF_spec98214; origin=EMBL - Metabolomics Core Facility Spectral Library",
  "num peaks": "7",
  "peaks": [
    ["103.054", "15"],
    ["107.049", "14"],
    ["120.081", "1000"],
    ["121.084", "16"],
    ["131.049", "41"],
    ["149.059", "16"],
    ["166.086", "56"]
  ]
}
```

Please see explanations of the keys in the MSP format.
