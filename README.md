# 🎬 MovieLens 25M: Collaborative Filtering Recommendation System

## Overview

This project presents a comparative analysis of collaborative filtering algorithms for movie recommendation using the [MovieLens 25M dataset](https://grouplens.org/datasets/movielens/25m/). We investigate whether **biased matrix factorization (SVD)** — a technique external to the CSCE 676 course syllabus — significantly outperforms **neighborhood-based collaborative filtering (Item-Item KNN)** for rating prediction, with a particular focus on how the performance gap varies across users with different activity levels.

Our analysis reveals that Biased SVD achieves statistically significant improvements in RMSE over both a bias-only baseline and Item-Item KNN, and that the performance advantage is largest for sparse users — those with the fewest ratings — validating the theoretical advantages of latent factor models in high-sparsity recommendation settings.

👉 **Start here:** [`main_notebook.ipynb`](main_notebook.ipynb)

🎥 **Project Video:** [Watch on YouTube](https://youtu.be/IlibDDKTZ1A)

---

## Research Question

> **"Does biased matrix factorization significantly outperform neighborhood-based collaborative filtering for rating prediction, and does the performance gap widen for sparse users?"**

This question is motivated by the extreme sparsity (99.74%) of the MovieLens 25M user-item matrix, which fundamentally limits neighborhood-based methods that depend on co-rating overlap.

---

## Data

**Dataset:** [MovieLens 25M](https://grouplens.org/datasets/movielens/25m/)  
**Source:** GroupLens Research, University of Minnesota  
**Size:** 25,000,095 ratings from 162,541 users across 59,047 movies (1995–2019)

**Key files used:**
- `ratings.csv` — userId, movieId, rating (0.5–5.0), timestamp
- `movies.csv` — movieId, title, genres

**Preprocessing:**
- The full 25M dataset is downloaded and extracted automatically by the notebook
- A **500,000-rating stratified sample** is used for modeling to balance computational cost with sufficient signal for latent factor learning
- Sample representativeness is validated against the full dataset (rating distribution, user activity, temporal coverage)

**Note:** The dataset is too large to include in the repository. The notebook automatically downloads it from the official source.

---

## How to Reproduce

This project was built entirely in **Google Colab**.

1. Open `main_notebook.ipynb` in Google Colab
2. Run all cells sequentially (Runtime → Run all)
3. The notebook will automatically download the MovieLens 25M dataset
4. All dependencies are available in the standard Colab environment; additional packages are installed inline

**Python version:** 3.11 (Google Colab default)

**Requirements:** See [`requirements.txt`](requirements.txt) for the full environment snapshot.

---

## Key Dependencies and Versions

| Package | Version | Purpose |
|---------|---------|---------|
| Python | 3.11 | Runtime |
| pandas | 2.2.2 | Data manipulation |
| numpy | 1.26.4 | Numerical computing |
| matplotlib | 3.9.2 | Visualization |

| scikit-surprise | 1.1.4 | Recommendation algorithms (SVD, KNN, BaselineOnly) |
| scikit-learn | 1.5.2 | PCA for latent factor visualization |
| scipy | 1.14.1 | Statistical significance testing |

Full dependency list available in `requirements.txt`.

---

## Repository Structure

```
movielens-recommendation-system/
├── README.md                      ← You are here
├── requirements.txt               ← Full Colab environment snapshot
├── .gitignore                     ← Excludes data files and temp artifacts
├── main_notebook.ipynb            ← 👉 Main deliverable notebook
└── checkpoints/
    ├── checkpoint_1.ipynb         ← Dataset comparison, selection & EDA
    └── checkpoint_2.ipynb         ← Research questions & feasibility runs
```

---

## Results Summary

| Finding | Evidence |
|---------|----------|
| **Biased SVD significantly outperforms Item-Item KNN** | Table 1: ~9.5% RMSE improvement over KNN |
| **The advantage is statistically significant** | 5-fold cross-validation with paired t-test (p < 0.05) |
| **Performance gap is largest for sparse users** | Stratified analysis by user activity quartile |
| **Bias terms capture meaningful rating patterns** | Distribution analysis of learned user/item biases |
| **Latent factors learn taste dimensions beyond genre** | PCA visualization of item factor vectors |

**Key takeaway:** Biased SVD's ability to learn compact latent representations makes it particularly effective in the extreme-sparsity regime characteristic of large-scale recommendation, where neighborhood methods struggle due to insufficient co-rating overlap.

---

## Collaboration and Resource Declaration

1. **Collaborators:** None
2. **Web Sources:**
   - MovieLens 25M: https://grouplens.org/datasets/movielens/25m/
   - Surprise library: https://surpriselib.com/
   - scikit-learn documentation: https://scikit-learn.org/
3. **AI Tools:** GitHub Copilot and ChatGPT were used for code debugging and documentation drafting
4. **References:** See the References section at the end of `main_notebook.ipynb`
