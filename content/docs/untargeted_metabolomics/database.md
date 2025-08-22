---
linkTitle: "About MS/MS database"
title: "MS/MS database"
weight: 4
---

## Introduction

A MS/MS database contains m/z, MS/MS spectrum, retentiont time and other information of known compounds. It will be used for compound annotation. You can either <u>download a MS/MS database</u> or <u>prepare your own database</u>.

MassCube uses unweighted entropy similarity for spectral matching based on the [ms_entropy](https://msentropy.readthedocs.io/en/latest/) Python package.

## Download a MS/MS database

You can [download](https://zenodo.org/records/15740986) a combined public MS/MS databases (including MassBank, GNPS, MS-DIAL and MassBank EU). The database is in .pkl format for faster loading speed in `masscube`.

## Prepare a database (for advanced users)

Three formats are supported for the database: pickle, msp, and json.

{{< callout emoji="🌐" >}}
We highly recommend generating the pickle (.pkl) format MS/MS database.
{{< /callout >}}

### MSP format

This is the most commonly used database format. Each block is one compound separated by a blank line.

{{< callout type="info" >}}
You must provide the MSP file with the keys examplified below.
{{< /callout >}}

```python
NAME: L-PHENYLALANINE                     # name
PRECURSORMZ: 166.0860                     # precursor m/z
PRECURSORTYPE: [M+H]+                     # adduct
IONMODE: positive                         # ion mode
RETENTIONTIME: 3.31                       # retention time in minutes
CCS: 136.82                               # collision cross section
FORMULA: C9H11NO2                         # chemical formula
SMILES: C1=CC=C(C=C1)C[C@@H](C(=O)O)N     # SMILES string
INCHIKEY: COLNVLDHVKWLRT-QMMMGPOBSA-N     # InChIKey
INSTRUMENTTYPE: LC-ESI-QFT                # instrument type
COLLISIONENERGY: 35.0 eV                  # collision energy
Num Peaks: 7                              # number of fragment signals
103.054	15                                # m/z and intensity of fragment signals
107.049	14
120.081	1000
121.084	16
131.049	41
149.059	16
166.086	56
```

NAME, PRECURSORMZ, PRECURSORTYPE, IONMODE, and fragment signals are mandatory.

### Pickle format

A .pkl database is a `FlashEntropySearch` object that contains the MS2 database. ms_entropy version 1.3.4 is highly recommended to generate this object (other versions may not work). Here is an example of how to generate a .pkl database from a msp file:

```python
from masscube.annotation import index_msp_to_pkl

# it will output a database.pkl file in the same folder
index_msp_to_pkl('database.msp')
```

Please refer to the source code of `index_msp_to_pkl` for more details.

### JSON format

A JSON database is a list of dictionaries. Each dictionary represents a compound with the following keys:

```python
dic = {
  "name": "L-PHENYLALANINE",                  # name
  "precursor_mz": 166.086013793945,           # precursor m/z
  "precursor_type": "[M+H]+",                 # adduct
  "ion_mode": "Positive",                     # ion mode
  "retention_time": "3.30520009994507",       # retention time in minutes
  "ccs": "136.819671630859",                  # collision cross section
  "formula": "C9H11NO2",                      # chemical formula
  "smiles": "C1=CC=C(C=C1)C[C@@H](C(=O)O)N",  # SMILES string
  "inchikey": "COLNVLDHVKWLRT-QMMMGPOBSA-N",  # InChIKey
  "instrument_type": "LC-ESI-QFT",            # instrument type
  "collision_energy": "35.0 eV",              # collision energy
  "num peaks": "7",                           # number of fragment signals
  "peaks": [                                  # fragment signals
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

To index a JSON database, you can use the `index_json_to_pkl` function:

```python
from masscube.annotation import index_json_to_pkl
index_json_to_pkl('database.json', 'database.pkl')
```

Please refer to the source code of `index_json_to_pkl` for more details.
