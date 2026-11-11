TEST_PASTE# CENG313 – Introduction to Data Science · Course Project

**Course organization:** [github.com/ceng313-2026](https://github.com/ceng313-2026)

Welcome! In this project your team takes part in a **Kaggle competition** and documents the
full data-science workflow on GitHub. All project repositories live in this organization,
where the instructor and teaching assistant can follow and evaluate your work.

---

## 1. Getting started

1. **Create a GitHub account** if you don't have one (use your university email if possible).
2. **Send your GitHub username** to the TA together with your **group ID** and group members.
3. **Accept the invitation** to the `ceng313-2026` organization (check your email or
   [github.com/notifications](https://github.com/notifications)).
4. **Join the Kaggle competition** with every team member (accept the competition rules
   so you can download the data). If the competition is still **active**, form a Kaggle team.

> **Closed competitions are fine.** Most closed Kaggle competitions still accept
> **Late Submissions** (*Submit Prediction* button on the competition page). A late
> submission gets a **public and private score**, but it is not placed on the leaderboard.
> See section 4 for what to do if your competition does not allow late submissions.

---

## 2. Moving your team repository into the organization

You have already created your project repository under your own account. Now **move it
into the course organization**. Nothing is lost: commits, branches and issues are kept,
and the old link redirects to the new one.

This is done **once per team, by the member who owns the repository**.

1. Make sure you have **accepted the organization invitation**.
2. Open your repo → **Settings → General → Danger Zone → Transfer ownership**.
3. Choose **Specify an organization** → `ceng313-2026`, type the repo name and click **Transfer**.
4. Keep the repository name in the course format **`GROUP{GROUP_ID}_CENG313`**
   (e.g. `GROUP07_CENG313`). If your name is different, fix it under
   **Settings → General → Repository name**.
5. Go to **Settings → Collaborators and teams** and check that **all team members** have
   **Write** access. Add anyone who is missing.
6. Every team member updates their local clone:
   ```bash
   git remote set-url origin https://github.com/ceng313-2026/GROUP{GROUP_ID}_CENG313.git
   git remote -v        # check the new address
   ```

> Repositories outside the organization will **not** be evaluated.
> If the transfer fails ("you don't have permission"), you have not accepted the
> invitation yet. Contact the TA if the problem continues.

---

## 3. Required repository structure

If your repository already has a different layout, reorganize it to match this structure
before Assignment 1.

```
GROUP{GROUP_ID}_CENG313/
├── README.md                          ← group, members, competition, how to run, scores
├── requirements.txt                   ← Python packages used
├── .gitignore                         ← must exclude data/
├── assignment1_eda_baseline.ipynb     ← Assignment 1: EDA & baseline
├── assignment2_solution.ipynb         ← Assignment 2: improved solution
├── src/
│   ├── __init__.py                    ← empty file, makes src importable
│   ├── data.py                        ← loading & preprocessing functions
│   ├── models.py                      ← model training & evaluation functions
│   └── utils.py                       ← helpers (plotting, metrics, saving submissions)
├── data/                              ← NOT committed (Kaggle rules + file size)
└── submissions/                       ← submission score screenshots
```

**Notebooks vs. `src/`:** notebooks tell the story (explanations, plots, results);
reusable code lives in `src/` and is imported, so both assignments use the same functions:

```python
from src.data import load_data, preprocess
from src.models import train_baseline
```

**Your own README must include:** group ID, member names and student IDs, the Kaggle
competition link, how to download the data, how to run the notebooks, and your current
Kaggle score (leaderboard or late-submission score).

---

## 4. Assignment 1 – EDA & Baseline (`assignment1_eda_baseline.ipynb`)

Your notebook must contain the following sections, each with **markdown explanations**:

| # | Section | What we expect |
|---|---------|----------------|
| 1 | Problem definition | Task, target variable, evaluation metric |
| 2 | Data overview | Shape, dtypes, `describe()`, missing values, duplicates |
| 3 | Exploratory data analysis | Distributions, outliers, target balance, relationships with the target — **every plot followed by a written interpretation** |
| 4 | Preprocessing | Cleaning, imputation, encoding, scaling — and **why** |
| 5 | Baseline model | A simple model (e.g. logistic/linear regression, decision tree), train/validation split, score on the competition metric |
| 6 | Kaggle submission | First submission and its score (screenshot in `submissions/`). Closed competition: a **late submission** with its public/private score |
| 7 | Conclusion | Key findings and next steps |

**If your competition does not accept late submissions** (or the test labels are not available):
- Hold out **20 % of `train.csv`** as your test set (`train_test_split(..., random_state=42)`,
  `stratify=y` for classification) and report your score on it with the **competition metric**.
- Compare it with the **top public scores** shown on the competition's leaderboard and
  with public notebooks, and write one sentence on how far you are from them.
- Note in your README: *"Competition closed — evaluated on a held-out split."*

---

## 5. How to submit

1. **Restart & Run All** — commit the notebook **with outputs saved**, so it can be read
   on GitHub without running it.
2. Do **not** commit the dataset. Load it with a relative path (`data/train.csv`) or the Kaggle API.
3. Push your final version and create a **tag** before the deadline:
   ```bash
   git add .
   git commit -m "Assignment 1: EDA and baseline"
   git tag assignment1
   git push origin main --tags
   ```
4. The **tagged version** is evaluated. Commits after the deadline are not considered.

> If GitHub cannot display your notebook, add an
> [nbviewer](https://nbviewer.org) or Colab link to your README.

---

## 6. Evaluation (Assignment 1)

| Criterion | Points |
|-----------|-------:|
| Problem, target & metric explained | 10 |
| Data overview (shape, types, missing values, duplicates) | 15 |
| EDA plots with written interpretation | 30 |
| Preprocessing decisions justified | 15 |
| Baseline model with validation score | 20 |
| Kaggle submission / score proof (or held-out evaluation) | 5 |
| Code quality, structure & README | 5 |
| **Total** | **100** |

- **Interpretation matters more than the number of plots.**
- Every member must have **meaningful commits**. Contributions are checked in
  *Insights → Contributors*.
- Feedback is given as a **GitHub Issue** titled *"Assignment 1 feedback"* in your repository.

---

## 7. Academic integrity

- **Do not use Kaggle notebooks directly.** Forking, downloading or copying a public Kaggle
  notebook — or copying **any of its cells** (code or markdown) — into your project is
  **not allowed**, even with a citation. Copied notebooks or cells receive **0 points**
  for that part.
- You may **read** public notebooks and discussions to get ideas. If an idea shaped your
  work (e.g. a feature or a plot type), **write the code yourself** and add the link in a
  markdown cell: *"Idea adapted from: <link>"*.
- Your notebooks must be written in **this repository** by your group, not in Kaggle's
  online editor and then exported. The commit history must show your work developing over time.
- Copying from other groups is plagiarism for **both** groups.
- Every member must be able to explain any cell in the notebook. Groups may be asked a
  short **oral question** about their work.

---

## 8. Important dates

| Assignment | Deadline |
|------------|----------|
| **Assignment 1 – EDA & Baseline** | **13 November 2026 (Friday), 23:59** |
| **Assignment 2 – Solution** | **30 December 2026 (Wednesday), 23:59** |

**Questions?** Open an issue in your repository or contact the teaching assistant.
