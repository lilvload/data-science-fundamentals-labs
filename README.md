# Data Science Fundamentals Labs

Laboratory works on the fundamentals of data science in Python, written as Jupyter notebooks.

The five labs follow the basic steps of working with data: exploring a dataset with pandas, selecting and editing data, cleaning missing values, training a first regression model and clustering customers. Each lab works on its own real-world dataset (IMDb movies, European football teams, Titanic passengers, salaries, wholesale customers).

> **Note:** code is in Python, while markdown explanations and chart labels in the notebooks are in Ukrainian.

## Contents

| Lab | Topic | Dataset | Main tools |
|-----|-------|---------|------------|
| [Lab 1](lab-1/lab-1.ipynb) | Summary functions, mappings and column operations | IMDb top rated movies | pandas, NumPy |
| [Lab 2](lab-2/lab-2.ipynb) | Indexing, selecting and editing data | 2021-2022 football team stats | pandas |
| [Lab 3](lab-3/lab-3.ipynb) | Detecting and handling missing data | Titanic passengers | pandas, seaborn |
| [Lab 4](lab-4/lab-4.ipynb) | Linear regression: salary vs. years of experience | Salary dataset | scikit-learn, seaborn |
| [Lab 5](lab-5/lab-5.ipynb) | K-means clustering of customers | Wholesale customers | scikit-learn, Matplotlib |

## Repository structure

```
data-science-fundamentals-labs/
├── lab-1/   lab-1.ipynb, imdb-top-rated-movies-user-rated.csv
├── lab-2/   lab-2.ipynb, 2021-2022 Football Team Stats.csv
├── lab-3/   lab-3.ipynb, titanic.csv
├── lab-4/   lab-4.ipynb, salary.csv, train.csv, test.csv
└── lab-5/   lab-5.ipynb, Wholesale customers data.csv
```

Each folder is self-contained: the notebook sits next to the CSV file it reads. The notebooks are committed with their outputs, so tables and charts can be viewed on GitHub without running anything.

## Labs

### Lab 1. Summary functions and mappings

Explores a dataset of about 950 top rated IMDb movies (rating, votes, Meta Score, director, writers, stars, gross).

- Applies **summary functions** to columns: `describe()`, `mode()`, `count()` and `value_counts()` (for example, the ten directors with the most movies in the list).
- Uses **mappings**: `map()` to shift the Meta Score of Quentin Tarantino's movies, and `apply()` with a row function that centres the IMDb rating and Meta Score around chosen means (Akira Kurosawa's average rating and the mean of Meta Scores above 50).
- Shows **built-in column operations**: arithmetic between a column and a constant, and concatenation of two columns into a "Title - Director" string.

### Lab 2. Indexing, selecting and editing data

Works with 2021-2022 statistics of the teams of the five top European leagues (Premier League, Ligue 1, Bundesliga, Serie A, La Liga): points, goals, expected goals (xG), attendance, top scorer and goalkeeper.

- Accesses columns **as attributes and as dictionary keys**, and single elements by index.
- Demonstrates **index-based selection** with `iloc`: rows, columns, slices and slices with a step.
- Demonstrates **label-based selection** with `loc`: single values, lists of columns and row ranges with a step.
- Sets a custom index with `set_index('Squad')`.
- Filters data with **conditional selection**: a simple condition (attendance above the median), compound conditions with `&`, `isin()` and `isnull()`.
- **Edits the data**: splits the "Top Team Scorer" column into the player's name and number of goals, drops and renames columns, and sorts by goals.

### Lab 3. Handling missing data

Cleans the classic Titanic passenger dataset (891 rows).

- Visualises missing values with a seaborn **heatmap** and counts them per column.
- **Age:** a boxplot shows that age depends on ticket class, so missing ages are filled with the **median age of the passenger's class**.
- **Cabin:** most values are missing, so two strategies are compared: dropping the column completely, or turning it into a binary feature (1 if a cabin is known, 0 if not). The notebook keeps the binary feature.
- **Embarked:** only two values are missing, so those rows are dropped.
- Confirms with a final heatmap and counts that the dataset has no missing values left.

### Lab 4. Linear regression

Predicts an employee's annual salary from years of experience (375 records).

- Explores the data with `info()` and `describe()`, drops rows with missing values and plots a scatter chart.
- Splits the data into training and test sets (70/30) with `train_test_split`.
- Trains a scikit-learn **`LinearRegression`** model and draws the fitted line over the test points.
- Evaluates the model with **MAE, MSE, RMSE and R²**.

On the saved run the model reached R² ≈ 0.87 and RMSE ≈ 17,100 USD. The folder also contains `train.csv` and `test.csv` (simple x/y data), which the notebook does not use.

### Lab 5. K-means clustering

Segments the clients of a wholesale distributor by their annual spending (440 customers).

- Loads the data and takes two features: annual spending on **Fresh** products and on **Milk** products.
- Uses the **elbow method** (inertia for 1 to 10 clusters) to choose the number of clusters, which gives 4.
- Trains a scikit-learn **`KMeans`** model with `k-means++` initialisation.
- Plots the four customer clusters and their centroids.

## Getting started

1. Clone the repository:

   ```bash
   git clone https://github.com/lilvload/data-science-fundamentals-labs.git
   cd data-science-fundamentals-labs
   ```

2. Create a virtual environment and install the dependencies:

   ```bash
   python -m venv .venv
   source .venv/bin/activate        # Windows: .venv\Scripts\activate

   pip install numpy pandas matplotlib seaborn scikit-learn jupyter
   ```

3. Start Jupyter and open a notebook:

   ```bash
   jupyter notebook
   ```

   The notebooks read their CSV files by relative path, so open each one from its own folder (Jupyter does this automatically). They were written with Python 3.12.

### Notes on running

- **Lab 1** has a typo in one cell: `movies[movies['Director'] = 'Akira Kurosawa']` uses `=` instead of `==` and raises a `SyntaxError`. The other cells still run; replace `=` with `==` to fix it.
- **Lab 2** reads its CSV with `delimiter=';'` and `encoding='latin-1'`, because the file uses semicolons and is not UTF-8.

## Technologies

Python · Jupyter · pandas · NumPy · Matplotlib · seaborn · scikit-learn
