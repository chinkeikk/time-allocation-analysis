# Time Allocation Patterns in the United States

Analysis of how Americans allocate their daily time across activities, how these patterns differ by income level, and how they changed during the COVID-19 pandemic.

**Course**: SP26 Usable AI — Midterm Project
**Team**: Qingyi Ren, Junqi Li, Zhanqi Li, Tzu-Ching Kuo

## Research Questions

1. How did daily time allocation patterns change before and during the COVID-19 pandemic (pre-2020 vs. 2020–2021)?
2. Can daily time allocation patterns predict a person's income group?

## Dataset

- **Source**: [American Time Use Survey (ATUS), 2003–2021](https://docs.google.com/spreadsheets/d/1PlpKLPoT1ppbWohBSwybnGCEP7_mHLrv/edit?gid=1079022340)
- Conducted by the U.S. Bureau of Labor Statistics
- 228,455 survey records across 18 years
- 31 columns: 8 demographic variables + 23 activity time variables (recorded in minutes per day)

## Methods

- **Data cleaning**: Removed records with missing or refused income; dropped Occupation Type column due to high missingness
- **Feature engineering**: Grouped income into 4 brackets (Low <$20K, Lower-Mid, Upper-Mid, High >$100K); split data into Pre-COVID (≤2019) vs. COVID (2020–2021)
- **Exploratory analysis**: Compared average daily hours across 6 core activities (Work, Leisure, Household, Exercise, TV, Sleep) by income group and time period
- **Statistical testing**: Independent t-tests on Pre-COVID vs. COVID activity differences
- **Regression**: OLS regression with controls for age, sex, employment status, and income group to isolate COVID effect
- **Classification**: Logistic Regression and Random Forest to predict income group from time use
- **Clustering**: K-means (k=3) to identify lifestyle groups (Household-focused, Work-heavy, Leisure-dominant)

## Project Structure

```
.
├── time-allocation-analysis.ipynb        # Main analysis notebook
├── American Time Use Survey.xlsx  # Dataset (see note below if missing)
├── requirements.txt               # Python dependencies
└── README.md
```

## Setup & Running the Code

### Prerequisites

- Python 3.11 (the notebook was developed on 3.11.14)
- Jupyter Notebook or JupyterLab

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/time-allocation-analysis.git
cd time-allocation-analysis
```

### 2. Create a virtual environment (recommended)

```bash
python -m venv venv
# macOS / Linux
source venv/bin/activate
# Windows
venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Get the dataset

If `American Time Use Survey.xlsx` is not in the repository (file size limits), download it from the [ATUS dataset link](https://docs.google.com/spreadsheets/d/1PlpKLPoT1ppbWohBSwybnGCEP7_mHLrv/edit?gid=1079022340) and place it in the project root with the exact filename `American Time Use Survey.xlsx`.

### 5. Run the notebook

```bash
jupyter notebook Final_Q1_Analysis.ipynb
```

Then run all cells from top to bottom (Cell → Run All).

## Key Findings

- Higher income groups spend more time working; lower income groups spend more time on leisure and TV
- During COVID, work time decreased while leisure, household activities, TV, and sleep all increased (all changes statistically significant, p < 0.05)
- TV watching showed the largest COVID-era increase (+0.40 hrs/day)
- Income group prediction from time use alone achieved ~32% accuracy (Random Forest) — better than the 25% random baseline but suggests time use overlaps significantly across income groups
- K-means clustering revealed 3 natural lifestyle groups: Household-focused, Work-heavy, and Leisure-dominant

## Dependencies

See `requirements.txt`. Main libraries: pandas, numpy, scikit-learn, matplotlib, seaborn, scipy, statsmodels, openpyxl.
