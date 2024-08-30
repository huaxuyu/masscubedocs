---
title: "feature_table_utils.py"
weight: 1
---

This utility module provides functions for manipulating and exporting feature tables in metabolomics data analysis. It focuses on converting feature lists to DataFrame format and exporting MS2 spectra to the MSP format. Below are detailed descriptions of the provided functions.

### output_feature_to_msp

`output_feature_to_msp(feature_table, output_path)`

**Purpose:**  
This function exports MS2 spectra from a DataFrame to the MSP format, which is commonly used in metabolomics for sharing spectral data.

**Parameters:**

- `feature_table` (`pandas.DataFrame`): The DataFrame containing MS2 spectra data.
- `output_path` (`str`): The path where the MSP file will be saved.

**Functionality:**

- Checks if the provided output path ends with `.msp` and raises a `ValueError` if not.
- Iterates through the rows of the `feature_table` DataFrame.
- For each feature, it writes the relevant information (e.g., precursor m/z, adduct type, retention time) and MS2 peaks to the MSP file.
- Handles cases where no MS2 spectrum is available by writing a default "Unknown" entry.

**Example Usage:**

```python
output_feature_to_msp(feature_table, "output.msp")
```

---

### convert_features_to_df

`convert_features_to_df(features, sample_names)`

**Purpose:**  
This function converts a list of feature objects into a pandas DataFrame, which is useful for further data analysis or export.

**Parameters:**

- `features` (`list`): A list of feature objects, each representing a detected metabolite or compound.
- `sample_names` (`list` or `array`): A list of sample names corresponding to the columns in the DataFrame.

**Returns:**

- `feature_table` (`pandas.DataFrame`): A DataFrame where each row corresponds to a feature, and the columns contain metadata and intensity values across samples.

**Functionality:**

- Collects various attributes of each feature, such as m/z, retention time, adduct type, and any annotation information.
- Includes additional columns for sample-specific peak heights.
- Returns the constructed DataFrame, which is structured for easy export or further analysis.

**Example Usage:**

```python
feature_df = convert_features_to_df(features, sample_names)
```

---

### **Example Workflow**

1. **Convert Features to DataFrame:**

   Suppose you have a list of feature objects detected during a metabolomics study. You can convert these features into a DataFrame for easier manipulation and analysis.

   ```python
   feature_df = convert_features_to_df(features, sample_names)
   ```

2. **Export MS2 Spectra to MSP:**

   After converting the features to a DataFrame, you might want to export the MS2 spectra data to an MSP file for use in spectral databases or other analysis tools.

   ```python
   output_feature_to_msp(feature_df, "output_data.msp")
   ```

---

These utility functions are designed to streamline the process of handling and exporting feature data in metabolomics workflows, particularly when dealing with large datasets and the need for standardized formats like MSP.
