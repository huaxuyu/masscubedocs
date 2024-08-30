---
title: "classifier_builder.py"
weight: 1
---

This module, `classifier_builder.py`, provides a set of tools for building and using a random forest classifier for metabolomics data analysis. It supports feature selection, model training, cross-validation, and prediction on new data. Below is a detailed breakdown of the functionality provided.

### **Module Overview**

This module is designed to help users build and use a random forest classification model from metabolomics data. It integrates data processing, feature selection, model training, cross-validation, and prediction. The module supports various steps, including untargeted metabolomics workflows and utility functions for managing data.

---

### **Key Functions**

#### **Helper Functions**

1. **`feature_selection(X, y, k=None)`**

   - **Purpose:** Selects the top `k` features based on statistical tests.
   - **Parameters:**
     - `X`: Feature matrix.
     - `y`: Target variable.
     - `k`: Number of features to select.
   - **Returns:** Selected features and their indices.

2. **`train_rdf_model(X_train, y_train)`**

   - **Purpose:** Trains a random forest classifier.
   - **Parameters:**
     - `X_train`: Training feature matrix.
     - `y_train`: Training target variable.
   - **Returns:** Trained random forest model.

3. **`cross_validate_model(X, y, model, k=5, random_state=0)`**

   - **Purpose:** Performs k-fold cross-validation on the model.
   - **Parameters:**
     - `X`: Feature matrix.
     - `y`: Target variable.
     - `model`: Trained random forest model.
     - `k`: Number of folds.
     - `random_state`: Random state for reproducibility.
   - **Returns:** List of accuracy scores for each fold.

4. **`predict(model, X_test)`**

   - **Purpose:** Predicts the class labels for test data.
   - **Parameters:**
     - `model`: Trained random forest model.
     - `X_test`: Test feature matrix.
   - **Returns:** Predicted class labels.

5. **`evaluate_model(predictions, y_test)`**
   - **Purpose:** Evaluates the model's performance using accuracy.
   - **Parameters:**
     - `predictions`: Predicted class labels.
     - `y_test`: True class labels.
   - **Returns:** Accuracy score.

#### **Main Functions**

1. **`build_classifier(path=None, feature_num=None, gaussian_cutoff=0.6, fill_percentage_cutoff=0.9, fill_ratio=0.5, cross_validation_k=5, data_processed=False)`**

   - **Purpose:** Builds a random forest classifier from raw or processed data.
   - **Parameters:**
     - `path`: Project path.
     - `feature_num`: Number of features to select.
     - `gaussian_cutoff`: Cutoff for Gaussian similarity.
     - `fill_percentage_cutoff`: Minimum percentage of non-zero values to retain a feature.
     - `fill_ratio`: Ratio to replace zero values in the data.
     - `cross_validation_k`: Number of folds for cross-validation.
     - `data_processed`: Flag to indicate if the data is already processed.
   - **Outputs:** Saves the trained model, selected features, and evaluation metrics.

   **Usage:**

   ```python
   build_classifier(path="/path/to/project", feature_num=50)
   ```

2. **`predict_samples(path, mz_tol=0.01, rt_tol=0.3)`**

   - **Purpose:** Predicts sample classes using the trained model.
   - **Parameters:**
     - `path`: Project path.
     - `mz_tol`: m/z tolerance for matching features.
     - `rt_tol`: Retention time tolerance for matching features.
   - **Outputs:** Saves predictions in the specified project path.

   **Usage:**

   ```python
   predict_samples(path="/path/to/project")
   ```

---

### **Workflow Integration**

- **`untargeted_metabolomics_workflow`:** This function, called within `build_classifier` and `predict_samples`, processes raw metabolomics data and prepares it for model building or prediction.

### **Example Usage**

1. **Building a Classifier:**

   ```python
   build_classifier(path="/path/to/project", feature_num=100, gaussian_cutoff=0.7, cross_validation_k=10)
   ```

2. **Predicting New Samples:**

   ```python
   predict_samples(path="/path/to/project")
   ```

---

### **Dependencies**

Ensure that the following Python packages are installed:

- `scikit-learn`, `pandas`, `numpy`, `os`, `pickle`, `shutil`

This module is designed to be used in metabolomics projects, providing a comprehensive approach to feature selection, model training, and prediction using random forest classifiers. It leverages the untargeted metabolomics workflow for data preparation and supports automated processing and analysis.
