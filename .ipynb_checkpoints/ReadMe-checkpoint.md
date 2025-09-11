# The Ugly Professor? Professor evaluations vs physical appearance

## The questions to be explored in the following analysis are relatively simple ones: 
- Do professors with higher "beauty" ratings also tend to receive higher evaluations, as instructors, by their students?
- Do males or females get higher evaluations from their students?

## Live project page: https://uglyprof.carrd.co/
## Repo: https://github.com/markcoty/Professor-eval-vs-appearance

## Highlights

- **Dataset:** The data are gathered from student evaluations for 463 courses taught by a sample of 94 professors from the University of Texas at Austin. Also, six students rate the professors' physical appearance. The result is a data frame where each row contains a different course and each column has information on the course and the professor who taught that course. 
- **Exploratory findings:**
  - Only about 14% of the professors are minority.
  - Males exceed females by about 15%.
  - Only 6% of the professors attended non-English speaking institutions.
  - About 2/3 of the classes were upper-level.
  - About 2/3 of the courses had multiple professors teaching them.
  - Almost all courses were multi-credit.
  - Only about 17% of the professors were formally dressed in their photos.
  - Only about 17% of the photos were in black-and-white.
  -  Score shows a mean attractiveness of 4.17, with a strong left-skew. This is an important number.
  - Age shows a mean of about 48, and is quite irregularly distributed.
  - About 74% of students completed professor evaluations, very left-skewed shape.
  - About 37 was the mean number of students in a class that did the evaluations, very right skewed (could be due to class sizes).
  - 55 was the mean class size, again very right-skewed, as in the previous case.
  - The mean beauty ratings given by each of the six judges were:
   - Lower-level female: 3.96
   - Upper-level female 1: 5.02
   - Upper-level female 2: 5.21
   - Lower-level male: 3.41
   - Upper-level male 1: 4.15
   - Upper-level male 2: 4.75
 - Overall average beauty rating: 4.42

- **Modeling:** 
 - All models are in the 0.65–0.68 accuracy range (except Logistic Regression at ~0.59–0.61).
 - This suggests the problem is not trivial, but also not highly separable by these models with the current features.
 - SVC: Highest recall (0.82 test, 0.83 CV), meaning it catches most positives, but at the cost of false positives (low TN).
 - Decision Tree: Highest precision (0.74 test, 0.73 CV), meaning when it predicts positive, it’s more likely to be correct, but it misses more positives (lower recall).
 - Random Forest / XGBoost: More balanced between precision and recall (~0.69 each).
 - If missing positives was costly, SVC would be better.
 - If false alarms were costly, Decision Tree would be better.
 - For a middle ground, Random Forest / XGBoost would be best.

- **Linear Regression Highlights**

 - Slope:
   - Female: 0.03 → For each 1-unit increase in beauty rating, average evaluation increases by only 0.03 points (very small effect).
   - Male: 0.11 → For each 1-unit increase in beauty rating, evaluations increase by 0.11 points (larger effect).
   - Interpretation: Beauty has a stronger positive relationship with evaluation scores for male professors.

 - Correlation:
   - Female: 0.09 → very weak correlation (close to zero).
   - Male: 0.31 → moderate positive correlation.
   - Interpretation: Male professors’ scores show a more noticeable upward trend with beauty ratings, whereas female professors’ scores barely change with beauty.

 - p-value:
   - Female: 0.2348 → not statistically significant (greater than 0.05). The slope could easily be due to chance.
   - Male: 2.0E(-7) → highly statistically significant. The relationship is very unlikely due to chance.
   - Interpretation: Beauty significantly predicts evaluations for male professors, but not for female professors.

- **Statistical tests:** Two-sample t-tests show that males have higher scores, and our confidence in this concluion is 99.7%.

🎯 **What I learned:** Cleaning/EDA on a complex set with some irrelevant variables; careful handling of imbalanced labels; building simple, reproducible ML baselines; packaging results for a portfolio.

**Repo Structure**

- ├─ Notebook/
- │ └─ Professor-eval-vs-appearance.ipynb (EDA → models → tests)
- ├─ Images/ 
- ├─ Data/ 
- ├─ requirements.txt
- └─ README.md

## Quickstart ##

**Environment**
[bash]
python -m venv .venv && source .venv/bin/activate   # (Windows: .venv\Scripts\activate)
pip install -r requirements.txt

**Data:**
Download the CSV from Kaggle (see Data folder or project page) and place it at Data/spotify.csv.

**Run:**
Open and run Notebook/light-spotify-dataset-v2.ipynb top-to-bottom.

**Reproducibility:**
Fixed random seed for all splits and models.
Stratified train/test split on the Explicit label.
All charts are saved from the notebook into Images/ on execution.

**Methods:** (brief)
EDA: bar charts for categorical fields; histograms + correlations for numeric fields; selected bivariate plots (e.g., Energy vs. Loudness, Danceability vs. Tempo).

**Modeling:** Logistic Regression, Decision Tree, Random Forest, SVC, using a simple sklearn Pipeline; evaluation with accuracy, precision, recall, F1, ROC-AUC; confusion matrix.

**Statistical tests:** two-sample t-tests for relationships of interest

**Results:** (short)
 - Beauty rating is more significant for male course evaluation scores.
 - Males score higher in course evaluations than do females.

**Modeling:** Simpler models perform best, which is consistent with the CV F1 scores: LR > SVC > RF/XGBoost > DT.

**Limitations:**
- Only six students rated professors' "beauty."
- Models are baseline, not production systems.

**Author:**
L. Mark Coty – data engineer, mathematician, and history enthusiast exploring data through music.



For a fuller rendering of this ReadMe, along with a few details not shown here, visit this link:
### [Project Website](https://uglyprof.carrd.co/ "The Ugly Professor?")
