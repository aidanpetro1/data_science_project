# Phenotyping Autoimmune Hemolytic Anemia to Drive the First Step of Workup

BMIN5030 (Data Science for Biomedical Informatics) final project, Aidan Petrovich.

## What the project does

Autoimmune hemolytic anemia (AIHA) is often diagnosed late because the hemolysis workup (haptoglobin, LDH, indirect bilirubin, then a DAT) is only ordered when a clinician already suspects it. Using MIMIC-IV, this project:

1. Builds a computable phenotype for anemia, hemolysis, and AIHA from labs and ICD codes.
2. Measures how often anemic adults are worked up for hemolysis.
3. Trains a model (lasso logistic regression and random forest) that predicts hemolysis from the CBC, age, and sex, as a basis for a clinical decision support (CDS) alert recommending a hemolysis panel.
4. Evaluates the model at alert-rate thresholds and with a stricter hemolysis label.

## Files

| File | Contents |
|---|---|
| `final_project.qmd` | Quarto report: overview, introduction, methods, results, and all R code |
| `data_science_project.Rproj` | RStudio Project for the repository |
| `.gitignore` | Keeps R session files and MIMIC-IV data out of the repository |
| `README.md` | This file |

## Data

MIMIC-IV v3.1 (`hosp` module) from PhysioNet. The full release requires credentialed access and is not included in this repository. The analysis uses `patients`, `admissions`, `labevents`, `d_labitems`, `diagnoses_icd`, and `d_icd_diagnoses`.

## Running the analysis

1. Set `mimic_dir` in the setup chunk of `final_project.qmd` to the folder holding the MIMIC-IV `hosp` files (`*.csv.gz`). Pointing it at a folder named `data/mimic-iv-demo/hosp` downloads and uses the open 100-patient demo instead, which runs the code but is too small to train the model.
2. Install the R packages: `tidyverse`, `glmnet`, `ranger`, `pROC`, `rsample`.
3. Render `final_project.qmd`. The first run reads `labevents` in chunks and caches the needed lab results as `labs_long.rds` next to the `hosp` folder.

Counts between 1 and 9 are shown as "<10", per the PhysioNet data use agreement.
