# Machine Learning Algorithms — CMPT 459

Python implementations and experiments from CMPT 459 coursework, covering supervised classification with random forests and unsupervised clustering with K-means.

## Repository structure

| Path | Description |
| --- | --- |
| `main.py` | Command-line entry point for the random forest experiment |
| `random_forest.py` | Custom decision-tree and random-forest implementation |
| `data/train.csv`, `data/test.csv` | Classification datasets |
| `report.pdf` | Report accompanying the random forest work |
| `CMPT459_Assignment2/main.py` | Single-cell data preprocessing, PCA, and clustering experiment |
| `CMPT459_Assignment2/kmeans.py` | Custom K-means implementation |
| `CMPT459_Assignment2/report.pdf` | Clustering assignment report |
| `CMPT459_Assignment2/*.png` | Saved clustering plots |
| `CMPT459_ Assignment 1.pdf` | Assignment document |

## 1. Random forest classification

The root-level scripts implement a random forest classifier with configurable tree count, splitting criterion, maximum depth, minimum split size, and feature count. The entry point reads the provided training and test CSV files and prints evaluation results.

### Requirements

Python 3, pandas, and NumPy:

```bash
python -m pip install pandas numpy
```

### Run

From the repository root:

```bash
python main.py --train-data data/train.csv --test-data data/test.csv
```

Optional command-line arguments include:

```text
--n-classifiers    Number of trees (default: 1)
--criterion        Split criterion setting (default: entropy)
--maxdepth         Maximum tree depth (default: 5)
--min-sample-split Minimum split size (default: 20)
--max-features     Feature count setting (default: 12)
```

The implementation is coursework code and has not been verified against current library versions. In particular, inspect the splitting and prediction logic before relying on its output: the current tree-building code uses Gini impurity directly even when the criterion argument is set to entropy.

## 2. K-means clustering of single-cell data

The `CMPT459_Assignment2/` directory contains a custom K-means implementation and an experiment using single-cell RNA sequencing data. The workflow filters and normalizes cells, applies PCA, compares random versus K-means++ initialization over several cluster counts, computes silhouette scores, and saves plots.

### Requirements

Python 3 with NumPy, Matplotlib, scikit-learn, AnnData, and Scanpy:

```bash
python -m pip install numpy matplotlib scikit-learn anndata scanpy
```

### Run

The script expects a single-cell dataset in CSV format. Its default filename, `scRNAseq_human_pancreas.csv`, is **not included in this repository**. Supply an appropriate dataset separately.

From the assignment directory:

```bash
cd CMPT459_Assignment2
python main.py --data /path/to/scRNAseq_human_pancreas.csv
```

The script compares cluster counts from 2 through 9 and writes `kmeans.png`, `kmeans++.png`, and `ScatterPlot.png`.

The `--n-clusters` argument is parsed, but the experiment currently loops over a fixed range of cluster counts. Preprocessing also assumes the input data supports the configured cell and gene filters.

## Notes

These are educational implementations intended to explore algorithm mechanics, not production-ready machine learning packages. No automated test suite or reproducible environment lockfile is included. See the reports and source code for additional assignment context.
