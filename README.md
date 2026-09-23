# ml-algorithm-comparison

> This was my final year university project. The full codebase isn't published here, since it was submitted as academic coursework, but the project's design, implementation and results are summarized below.

## Overview

A C++ pipeline built from scratch to compare four classification algorithms — uniform KNN, Gaussian-weighted KNN, decision trees, and multiclass SVM — across two datasets of very different scale and complexity: the Iris dataset and the NIST handwritten digit database. Each model was evaluated using 5-fold cross-validation, with confusion matrices and per-class precision/recall reviewed alongside overall accuracy.

## Tech Used
- **Language:** C++ (Version 17)
- **Build:** CMake (Version 3.14)
- **Tests:** CTest, Catch2
- **Documentation:** Doxygen
- **External Code:** pbPlots (for graph plotting), stb_image.h (for processing .png images)

## Datasets

- **Iris dataset** — a small, low-dimensional benchmark, used to sanity-check each model's behaviour on a simple classification task.
- **NIST Special Database 19** — a much larger, high-dimensional handwritten digit dataset, used as the more realistic test of each algorithm's ability to generalize.

## Third-Party Code and Libraries

This project uses the following third-party software:

### stb_image.h
- **Author:** Sean Barrett
- **Description:** Single-header image loading library used for decoding PNG image files.
- **Usage in this project:** Loading grayscale image data from disk prior to normalization and model training.
- **License:** Public Domain / MIT License (dual-licensed)
- **Source:** https://github.com/nothings/stb

The `stb_image.h` library was included unmodified in the `product/external/stb/` directory, with all original copyright and license notices preserved.

### pbPlots

pbPlots is a lightweight C++ plotting library, used here to generate image-based visualisations of evaluation results directly from the codebase, including:

- metric comparison charts
- cross-validation result plots
- confusion matrix visualisations
- other evaluation-related graphs

## Results Summary

On the simpler Iris dataset, uniform KNN, Gaussian KNN and decision trees all performed strongly across 5-fold cross-validation (roughly 96–97% accuracy), while multiclass SVM lagged behind at around 87%, likely due to normalization issues rather than a fundamental weakness of the model.

The NIST digit dataset — larger and much higher-dimensional — gave a clearer picture of each algorithm's real-world generalization ability. Gaussian KNN was the standout performer at around 99.6% accuracy, with multiclass SVM also performing well (~93%). Uniform KNN was moderate (~81%), with visible confusion between visually similar digit classes. Decision trees, despite doing well on Iris, collapsed on NIST to around 14% accuracy — a single tree couldn't find meaningful splits in the higher-dimensional space, defaulting to predicting one class almost universally.

Cross-validation confirmed these results were stable across folds rather than artifacts of a lucky train/test split. The overall takeaway: no single algorithm was best across the board — a model's suitability depends heavily on the dataset's scale and dimensionality, and preprocessing choices mattered as much as the choice of algorithm itself.
