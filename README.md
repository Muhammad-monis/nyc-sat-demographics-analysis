# 🎓 NYC SAT Demographics Analysis

> Exploring how race, poverty, safety, gender, and language shape SAT outcomes across New York City public high schools.

---

## 📌 Overview

The SAT is widely used by colleges as a measure of academic potential — but is it really measuring merit alone? This project investigates whether demographic and socioeconomic factors at NYC public high schools correlate with average SAT scores, using open data published by New York City.

The analysis reveals that **poverty is the single most powerful predictor of SAT performance**, with race, language background, and school funding acting as compounding factors.

---

## 📁 Repository Structure

```
nyc-sat-demographics-analysis/
│
├── nyc_sat_demographics_analysis.ipynb   # Main analysis notebook
│
└── schools/
    ├── sat_results.csv                   # SAT scores by school
    ├── ap_2010.csv                       # AP exam results (2010)
    ├── class_size.csv                    # Class size by school
    ├── demographics.csv                  # School demographics snapshot
    ├── hs_directory.csv                  # High school directory + geo coords
    ├── survey_all.txt                    # School survey (general schools)
    └── survey_d75.txt                    # School survey (District 75 schools)
```

---

## 📊 Data Sources

All data is publicly available from the [NYC Open Data portal](https://opendata.cityofnewyork.us/):

| Dataset | Description |
|---|---|
| [SAT Results](https://data.cityofnewyork.us/Education/SAT-Results/f9bf-2cp4) | Math, Reading, Writing scores per school |
| [School Attendance](https://data.cityofnewyork.us/Education/School-Attendance-and-Enrollment-Statistics-by-Dis/7z8d-msnt) | Attendance & enrollment stats |
| [Class Size](https://data.cityofnewyork.us/Education/2010-2011-Class-Size-School-level-detail/urz7-pzb3) | Class size details (2010–11) |
| [AP Results](https://data.cityofnewyork.us/Education/AP-College-Board-2010-School-Level-Results/itfs-ms3e) | AP exam participation & scores |
| [Graduation Outcomes](https://data.cityofnewyork.us/Education/Graduation-Outcomes-Classes-Of-2005-2010-School-Le/vh2h-md7a) | Graduation rates by cohort |
| [Demographics](https://data.cityofnewyork.us/Education/School-Demographics-and-Accountability-Snapshot-20/ihfw-zy9j) | Race, gender, ELL, poverty breakdowns |
| [School Survey](https://data.cityofnewyork.us/Education/NYC-School-Survey-2011/mnz3-dyi8) | Parent, teacher & student perception surveys |

---

## 🔍 Key Findings

### 💰 Poverty is the strongest predictor
Schools with higher percentages of students receiving free or reduced-cost lunches (`frl_percent`) show a **strong negative correlation** with SAT scores. This is the clearest and most consistent signal in the entire dataset.

### 🌍 Race & Ethnicity
- Higher percentages of **white and Asian students** correlate **positively** with SAT scores.
- Higher percentages of **Black and Hispanic students** correlate **negatively** — but this largely reflects underlying poverty levels and school funding disparities, not inherent ability.
- Schools with >95% Hispanic enrollment primarily serve **recent immigrants**, explaining lower scores through language barriers rather than academic capacity.

### 🗣️ English Language Learners
The `ell_percent` (English Language Learner percentage) has one of the **strongest negative correlations** with SAT scores. The SAT is ~67% English comprehension-based, which structurally disadvantages non-native speakers.

### 🛡️ School Safety
Both student (`saf_s_11`) and teacher (`saf_t_11`) safety ratings **correlate positively** with SAT scores. Schools where students and teachers feel safe tend to perform better academically.

### 👩‍🎓 Gender
- Schools with a higher `female_per` correlate slightly positively with SAT scores.
- A cluster of high-female, high-SAT schools are **selective liberal arts institutions**.

### 📚 AP Participation
Schools where a higher proportion of students take AP exams (`ap_per`) tend to have higher SAT scores — reflecting a culture of academic preparation and access to advanced coursework.

### 🏫 School Size
Larger schools (by enrollment) perform slightly better on average — contradicting the assumption that smaller schools with more individual attention yield higher scores.

---

## 🛠️ Methodology

1. **Data ingestion** — 6 CSV files and 2 tab-separated survey files read into a dictionary of DataFrames.
2. **Cleaning & standardization** — DBN (school identifier) standardized across all datasets; SAT scores and AP figures converted to numeric.
3. **Condensing** — Duplicate DBN rows resolved via filtering (grade level, program type, cohort year) and groupby averaging.
4. **Merging** — All datasets joined on DBN using a combination of left joins (AP, graduation) and inner joins (class size, demographics, survey, directory). Nulls filled with column means.
5. **Correlation analysis** — Pearson correlations computed between `sat_score` and all numeric columns. Values with |r| > 0.25 explored further.
6. **Visualization** — Scatter plots, bar charts, and regression plots used to validate and communicate findings.

---

## 🧰 Tech Stack

- **Python 3**
- **pandas** — data manipulation and merging
- **NumPy** — numeric operations
- **Matplotlib** — base plotting
- **Seaborn** — statistical visualizations
- **re** — regex for coordinate extraction from location strings

---

## 🚀 Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/Muhammad-monis/nyc-sat-demographics-analysis.git
cd nyc-sat-demographics-analysis
```

### 2. Install dependencies
```bash
pip install pandas numpy matplotlib seaborn jupyter
```

### 3. Launch the notebook
```bash
jupyter notebook nyc_sat_demographics_analysis.ipynb
```

> Make sure the `schools/` folder with all CSV and TXT files is in the same directory as the notebook.

---

## 💡 Conclusions

While multiple demographic factors influence SAT scores, they largely funnel back to one root cause: **economic inequality**. Students in poverty face compounding disadvantages — under-funded schools, lack of AP course access, need to work outside school, nutritional deficits, and ESL resource costs. The SAT, as currently designed, functions less as a pure measure of academic aptitude and more as a **proxy for socioeconomic status**.

---

## 📄 License

This project uses publicly available data from NYC Open Data. The analysis and code in this repository are open for educational and research use.
