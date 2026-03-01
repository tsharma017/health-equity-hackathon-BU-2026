# Sexual Identity and Suicidal Ideation Among U.S. High School Students

**Boston University School of Public Health — Health Equity Hackathon 2026**  
**Author:** Tej Sharma  
**Date:** February 28, 2026

---

## What This Project Is About

This project investigates whether **sexual identity is associated with suicidal ideation**
among U.S. high school students, and whether **race/ethnicity confounds or modifies**
that relationship.

Data comes from the **2023 Youth Risk Behavior Survey (YRBS)** — a national CDC survey
of over 20,000 U.S. high school students.

---

## Research Question

> Are non-heterosexual or questioning students more likely to report suicidal ideation
> compared to heterosexual students? Does race/ethnicity change that relationship?

---

## Key Findings

| Result | Value |
|---|---|
| SI Prevalence — Heterosexual | ~20% |
| SI Prevalence — Non-Het/Questioning | ~45% |
| Crude Odds Ratio | 4.39 |
| Adjusted Odds Ratio | 3.35 |
| Confounding Present? | YES (23.5% change) |
| Effect Modification by Race? | NO (all interaction p > 0.05) |

**Bottom line:** Non-heterosexual and questioning youth had **3.35 times higher odds**
of suicidal ideation compared to heterosexual peers, after adjusting for race/ethnicity,
age, sex, low grades, and bullying. This association was consistent across all racial groups.

---

## Variables Used

| Role | Variable | Description |
|---|---|---|
| Exposure | `sexual_identity_cat` | 0 = Heterosexual, 1 = Non-Het/Questioning |
| Outcome | `SI` | 0 = No suicidal ideation, 1 = Yes |
| Confounder/EMM | `raceeth` | 8 racial/ethnic groups |
| Covariate | `age` | Age 14–18 (codes 3–7) |
| Covariate | `sex_clean` | 0 = Male, 1 = Female |
| Covariate | `lowgrades_clean` | 0 = Good grades, 1 = Low grades |
| Covariate | `bullied_clean` | 0 = Not bullied, 1 = Bullied at school |

---

## Analysis Steps and Why I Chose Each Approach

### 1. Data Cleaning
**What I did:** Removed 12–13 year olds, recoded all variables to clean binary/numeric format.  
**Why:** Younger students may not reliably self-report sexual identity. Clean numeric
variables are required for logistic regression in R.

### 2. Descriptive Statistics (Table 1)
**What I did:** Created an overall Table 1 and a Table 1 stratified by sexual identity.  
**Why:** Table 1 is standard in epidemiology papers. The stratified version shows whether
the two groups differ on other characteristics — revealing potential confounders.

### 3. Chi-Square Test
**What I did:** Tested whether SI prevalence differs between the two sexual identity groups.  
**Why:** Chi-square is the standard test for association between two categorical variables.
It gives a p-value to tell us if the difference is statistically significant.

### 4. Crude Odds Ratio (Logistic Regression)
**What I did:** Ran a simple logistic regression with only the exposure predicting the outcome.  
**Why:** The crude OR gives the raw, unadjusted strength of the association. It is always
reported alongside the adjusted OR so readers can see how much confounding was present.

### 5. Adjusted Odds Ratio (Multivariable Logistic Regression)
**What I did:** Added race/ethnicity, age, sex, low grades, and bullying as covariates.  
**Why:** These variables could confound the association. Adjusting for them gives a
cleaner, more accurate estimate of the true effect of sexual identity.

**Why `relevel()` for only raceeth and age?**  
These are the only variables with 3+ categories, requiring manual specification of
the reference group. Binary variables (sex, grades, bullying) automatically use 0 as
the reference — no `relevel()` needed.

### 6. Confounding Assessment
**What I did:** Compared crude OR (4.39) vs adjusted OR (3.35) — a 23.5% change.  
**Why:** The standard rule in epidemiology is: if the OR changes by more than 10%
after adjustment, confounding is present and you must report the adjusted OR.

### 7. Effect Modification Testing (Interaction Term)
**What I did:** Added `sexual_identity_cat * factor(raceeth)` to the model and checked
p-values of the interaction terms.  
**Why:** Effect modification means the association between exposure and outcome differs
by a third variable. Testing for it is essential before deciding whether to report one
overall OR or separate ORs for each racial group.

**Decision rule:**
- Any interaction p < 0.05 → effect modification present → report stratified ORs
- All interaction p > 0.05 → no effect modification → report one adjusted OR ✅

### 8. Visualizations
**What I created:**
- Prevalence bar chart by sexual identity group
- Forest plot comparing crude vs adjusted OR
- Publication-ready forest plot of all adjusted ORs
- Heatmap of SI prevalence by race and sexual identity

**Why:** Visualizations make findings accessible to a broader audience and are essential
for presentations and publications.

---

## What I Learned

This project taught me how to approach a complete epidemiological analysis from scratch:

- How to read and clean survey data with coded numeric responses
- The difference between crude and adjusted estimates — and why both matter
- What confounding means statistically and how to detect it (>10% change rule)
- How to test for effect modification using interaction terms
- How to decide between stratified models vs one adjusted model
- How to create publication-quality visualizations in ggplot2
- How to write a complete analysis in R Markdown with narrative explanation

This was my first experience with **survey/epidemiological data** — my background is in
sequencing/genomics data. I found that the core logic (exposure → outcome, control for
confounders) maps surprisingly well across both fields.

---

## Repository Structure

```
├── YRBS_Sexual_Identity_Suicidal_Ideation.Rmd   # Full analysis with code + narrative
├── YRBS_Sexual_Identity_Suicidal_Ideation.html  # Rendered HTML output
└── README.md                                     # This file
```

---

**Required R packages:**
```r
install.packages(c("readr", "dplyr", "ggplot2", "tableone", "table1"))
```

---

## Data Source

**CDC Youth Risk Behavior Survey (YRBS) 2023**  
A national school-based survey monitoring health behaviors among U.S. high school students.  
https://www.cdc.gov/yrbs

---

## Limitations

- **Selection bias:** School-based survey misses absent/homeless youth who may have
  higher SI rates
- **Information bias:** Self-reported data may underreport sexual identity and SI due
  to social desirability
- **Misclassification:** Single time-point measurement of fluid sexual identity may
  bias OR toward null
- **Residual confounding:** Unmeasured variables (family support, mental health history)
  may still confound the association

---

## Skills Demonstrated

`R` · `R Markdown` · `ggplot2` · `Logistic Regression` · `Epidemiological Methods`  
`Confounding Assessment` · `Effect Modification Testing` · `Data Cleaning` · `Public Health`

---

*Completed as part of the BU School of Public Health Health Equity Hackathon, February 2026*
