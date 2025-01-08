---
title: "classifier_builder"
weight: 1
---

## Overview

This module provides a set of tools for building and using a random forest classifier for metabolomics data analysis. It supports feature selection, model training, cross-validation, and prediction on new data.

## Functions

### feature_selection

`feature_selection(X, y, k=None)`

**Parameters:**

- `X` (numpy.ndarray): The feature matrix.
- `y` (numpy.ndarray): The target variable.
- `k` (int): The number of features to select. By default, it is set to the number of samples divided by 10 (1/10 rule) and rounded up.

**Returns:**

- `X_new` (numpy.ndarray): The selected features.
- `selected_features` (numpy.ndarray): The indices of the selected features.

def feature_selection(X, y, k=None):
"""
Select features for the classification model.

    Parameters
    ----------
    X : two-dimensional numpy array
        The feature matrix.
    y : one-dimensional numpy array
        The target variable.
    k : int
        The number of features to select. By default, it
        is set to the number of samples divided by 10 (1/10 rule)
        and rounded up.

    Returns
    -------
    X_new : two-dimensional numpy array
        The fit-transformed feature matrix.
    selected_features : one-dimensional numpy array
        The indices of the selected features.
    """

### train_rdf_model

`train_rdf_model(X_train, y_train)`

**Parameters:**

- `X_train` (numpy.ndarray): The feature matrix for training.
- `y_train` (numpy.ndarray): The target variable for training.

**Returns:**

- `model` (RandomForestClassifier): The trained random forest model.

### cross_validate_model

`cross_validate_model(X, y, model, k=5, random_state=0)`

**Parameters:**

- `X` (numpy.ndarray): The feature matrix.
- `y` (numpy.ndarray): The target variable.
- `model` (RandomForestClassifier): The trained random forest model.
- `k` (int): The number of folds for cross-validation.
- `random_state` (int): The random state for the shuffle in KFold.

**Returns:**

- `scores` (list): The accuracy scores for each fold.

### predict

`predict(model, X_test)`

**Parameters:**

- `model` (RandomForestClassifier): The trained random forest model.
- `X_test` (numpy.ndarray): The feature matrix for testing.

**Returns:**

- `predictions` (numpy.ndarray): The predicted classes.

### evaluate_model

`evaluate_model(predictions, y_test)`

**Parameters:**

- `predictions` (numpy.ndarray): The predicted classes.
- `y_test` (numpy.ndarray): The true classes.

**Returns:**

- `accuracy` (float): The accuracy of the model.

### build_classifier

`build_classifier(path=None, by_group=None, feature_num=None, gaussian_cutoff=0.6, detection_rate_cutoff=0.9, fill_ratio=0.5, cross_validation_k=5)`

**Parameters:**

- `path` (str): Path to the project file.
- `feature_num` (int): The number of features to select for building the model.
- `gaussian_cutoff` (float): The Gaussian similarity cutoff. Default is 0.6.
- `fill_ratio` (float): The zero values will be replaced by the minimum value in the feature matrix times fill_ratio. Default is 0.5.
- `cross_validation_k` (int): The number of folds for cross-validation. Default is 5.

### predict_samples

`predict_samples(path, mz_tol=0.01, rt_tol=0.3)`

**Parameters:**

- `path` (str): Path to the project file.
- `mz_tol` (float): The m/z tolerance for matching the features. Default is 0.01.
- `rt_tol` (float): The retention time tolerance for matching the features. Default is 0.3.
