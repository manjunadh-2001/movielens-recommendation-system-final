# Data

## MovieLens 25M Dataset

- **Source:** [GroupLens Research, University of Minnesota](https://grouplens.org/datasets/movielens/25m/)
- **Size:** 25,000,095 ratings from 162,541 users across 59,047 movies (1995–2019)
- **Download:** ~250MB zip file

### How data is obtained

The dataset is **downloaded automatically** by `main_notebook.ipynb` (Cell 3). No manual download is required.

```python
URL = 'https://files.grouplens.org/datasets/movielens/ml-25m.zip'
```

The notebook downloads, extracts, and loads the following files:

| File | Description |
|------|-------------|
| `ratings.csv` | userId, movieId, rating (0.5–5.0), timestamp |
| `movies.csv` | movieId, title, genres |

### Preprocessing

- **No missing values** in either file (verified in notebook Section 2.1)
- A **500,000-rating simple random sample** (`random_state=42`) is drawn for modeling
- Sample representativeness is validated against the full dataset (Section 5)

### Why data is not committed

The raw dataset is ~250MB (zipped), which exceeds GitHub's file size limits. The `.gitignore` excludes `*.csv` and `*.zip` files.
