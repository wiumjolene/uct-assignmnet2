# PPH7021F Assignment 2 – Air Pollution and Biostatistics

This repository contains the analysis, code and report for Assignment 2 of **PPH7021F: Introduction to Biostatistics** (University of Cape Town, Semester 1 2025). The assignment uses the **WHO Ambient Air Quality Database** to explore air pollution levels across cities, years and WHO regions. It also looks at whether population size modifies the link between region and high PM2.5 exposure.

The analysis covers:

- Descriptive statistics with tests for differences between years
- Comparing two independent groups (Shapiro–Wilk, Mann–Whitney U)
- Correlation (Spearman rank)
- Comparing more than two groups (Kruskal–Wallis)
- Prevalence and prevalence ratios with 95% confidence intervals
- Effect modification by population size (stratified analysis, chi-squared tests)

The analysis was done in **Python using pandas, numpy, scipy and statsmodels**, and the report was written in **LaTeX**.

---

# Repository Structure

```
.
├── assignment2.pdf               # Assignment brief
│
├── code/
│   ├── q1.ipynb … q6.ipynb       # One notebook per assignment question
│   ├── config.py                 # Data path and the two comparison years (2015, 2020)
│   ├── get_data.py               # DataLoader: loads data, bins population, filters years
│   └── data/
│       ├── WMXJOL001_dataset.csv # Individual assignment dataset
│       └── q1.xlsx               # Question 1 summary output
│
└── manuscript/
    ├── cover.tex                 # Main LaTeX document
    ├── plagiarism.tex            # Plagiarism declaration
    ├── q1.tex … q6.tex           # One section per question
    ├── img/                      # Figures used in the report
    └── 20250427 - Jolene Wium - PPH7021F Assignment2 - Answers_v01.pdf   # Final report
```

---

# Dataset

`code/data/WMXJOL001_dataset.csv` is an individual extract of the WHO Ambient Air Quality Database. It has about 13,700 city-year records. The main variables are:

| Variable | Description |
|---|---|
| `who_region` | WHO region (e.g. `1_Afr`, `2_Amr`, `4_Eur`) |
| `country_name`, `city` | Location |
| `year` | Year of measurement |
| `pm10_concentration` | Annual mean PM10 (µg/m³) |
| `pm25_concentration` | Annual mean PM2.5 (µg/m³) |
| `no2_concentration` | Annual mean NO₂ (µg/m³) |
| `pm25_tempcov` | Temporal coverage of PM2.5 measurements (%) |
| `population` | City population |

Variables built from Assignment 1:

- **Population size categories**, in 500,000-wide bins.
- **PM2.5 exposure categories** (5 or less, 5–10, 10–15, 15–25, 25–30, and over 30 µg/m³), based on WHO guideline levels.

---

# Questions and Methods

| Q | Question | Method |
|---|---|---|
| 1 | Descriptive statistics overall and by year (2015 vs 2020) | Means and SDs, with p-values for differences between years |
| 2 | Is PM2.5 different between 2015 and 2020? | Shapiro–Wilk normality check, then a Mann–Whitney U test (independent samples) |
| 3 | Is year (continuous) associated with PM2.5? | Scatter plot (log scale) and Spearman rank correlation |
| 4 | Does PM10 differ by WHO region (2020)? | Box plot, Shapiro–Wilk, then a Kruskal–Wallis test across six independent groups |
| 5 | Is WHO region associated with PM2.5 exposure category (2018)? | Bar chart, prevalence of the highest category, and the prevalence ratio (1_Afr vs 4_Eur) with 95% CI |
| 6 | Does population size modify the region–exposure link? | Tables stratified by population category, stratum-specific prevalence and chi-squared tests |

---

# Key Results

- **Q1–2:** PM10, PM2.5 and NO₂ were all lower in 2020 than in 2015. PM2.5 was not normally distributed, and a Mann–Whitney U test showed a significant difference between the two years (p < 0.05).
- **Q3:** there was a weak negative correlation between year and PM2.5 (Spearman ρ = −0.163, p < 0.05).
- **Q4:** PM10 differed significantly across WHO regions in 2020 (Kruskal–Wallis p < 0.05).
- **Q5:** in 2018, 6.7% of cities were in the highest PM2.5 category (over 30 µg/m³), compared with 2% in 4_Eur. 1_Afr had only one city in the sample, so the prevalence ratio is very imprecise.
- **Q6:** in 4_Eur, the prevalence of high PM2.5 exposure rose with population size (3.5%, 4.0% and 16.7% across the first three categories). This was read as evidence of effect modification, so the stratified estimates were chosen for reporting.

The full answers are in the final report in `manuscript/`.

---

# Requirements

Python packages used:

1. pandas
1. numpy
1. scipy
1. statsmodels
1. matplotlib
1. openpyxl
1. jupyter

Install them with:

```bash
pip install pandas numpy scipy statsmodels matplotlib openpyxl jupyter
```

The report needs a LaTeX distribution (e.g. MiKTeX or TeX Live) to build.

---

# Running the Analysis

1. Open the notebooks in `code/` and run them in order (`q1.ipynb` to `q6.ipynb`). The comparison years are set in `config.py`.
2. Build the report from `manuscript/cover.tex`:

```bash
cd manuscript
latexmk -pdf cover.tex
```
