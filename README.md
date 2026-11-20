# NESA: Shared Task on Low-resource Essay Scoring at CHiPSAL-IndoNLP 2027

**Competition link:** [Codabench](https://www.codabench.org/competitions/18661/)

**Automated essay scoring for a low-resource language**

Automated essay scoring (AES) is well studied for English and a few other high-resource languages, but Nepali, spoken by more than 30 million people, had no scoring benchmark until recently. This shared task asks participants to build systems that score Nepali student essays the way expert teachers do. The shared task is part of the CHiPSAL-IndoNLP 2027 workshop at COLING 2027, and the competition is hosted on Codabench.

## Task

Given the text of a Nepali essay, predict its holistic score: an integer from 1 to 10.

The data comes from **NESA** (Nepali Essay Scoring Assessment), the first expert-annotated dataset of Nepali student essays (Thapa et al., 2025). Students in grades 8, 9 and 10 all wrote on the same topic, *Discipline* (अनुशासन), in about 35 minutes. Expert Nepali teachers scored each essay holistically on a 1–10 scale, following a rubric covering content relevance, structure, clarity and language fluency. Disagreements of more than one point were settled by a third teacher.

| Score | What it typically means |
|-------|-------------------------|
| 1–3 | Incomplete or incoherent |
| 4–6 | Average: moderate organization and clarity |
| 7–10 | Well structured, grammatically sound and contextually rich |

**To learn more about the dataset**, see the [dataset paper](https://doi.org/10.1109/BIGDATA66926.2025.11402339).

## Participation

Join the competition on Codabench: [NESA: Shared Task on Low-resource Essay Scoring](https://www.codabench.org/competitions/18661/)

The competition has two phases:

* **Development phase:** train on the training data and submit predictions for the eval essays. Scores appear on the leaderboard.
* **Test phase:** submit predictions for the test essays. Your **last** submission in this phase is the one that is ranked.

## Dataset

Every essay has a unique identifier, `id`. All files are UTF-8 CSV. Essays can span several lines, so read the files with a proper CSV parser (for example `pandas.read_csv`).

| Data | Files | Essays | Columns | Link |
|------|-------|--------|---------|------|
| Train | `train.csv` | 341 | `id`, `text`, `label` | [Link](https://drive.google.com/drive/folders/1-rmhS2KpOnUla-PSm2fBe1Ny8yMV2q99?usp=sharing) |
| Eval | `eval.csv`, `sample_submission_eval.csv` | 72 | `id`, `text` | [Link](https://drive.google.com/drive/folders/1vc6QlxOP4EWss-yUh7DvB4Db1pFcvkYi?usp=sharing) |
| Test | `test.csv`, `sample_submission_test.csv` | 72 | `id`, `text` | Released on Jan 4, 2027 |

`label` is the teachers' score, an integer from 1 to 10. Most essays score between 3 and 6; scores of 9 and 10 are rare.

## Use of External Data

External datasets and pretrained models are allowed. Describe any external data you use in your system description paper.

## Evaluation

Submissions are ranked by **Quadratic Weighted Kappa (QWK)** between your scores and the teachers' scores. QWK is 1 for perfect agreement and 0 for chance-level agreement, and it penalizes a disagreement by the square of its size. It is computed over the fixed 1–10 scale:

```python
from sklearn.metrics import cohen_kappa_score
qwk = cohen_kappa_score(gold, predicted, labels=list(range(1, 11)), weights="quadratic")
```

The leaderboard also shows the **Mean Absolute Error (MAE)**, for information only.

## Submission Format

Your submission file must be a CSV file named `predictions.csv` with the columns `id` and `label`, one row for every essay in the current phase (`eval.csv` in the Development phase, `test.csv` in the Test phase). `label` must be an integer from 1 to 10. Zip the file and submit the zip.

| id | label |
|----|-------|
| 1322 | 2 |
| 1334 | 8 |
| 1668 | 2 |

A sample submission for the Development phase is in this repository: [sample_submission.csv](sample_submission.csv). To check your setup, rename it to `predictions.csv`, zip it, and submit it to the Development phase.

If something is wrong with your file (missing ids, ids from the other phase, scores outside 1–10, duplicate rows), the submission fails. Click it on Codabench and open the **Scoring errors** tab to see what to fix. Failed submissions don't count toward your limit.

## Publication

Participants in the shared task are expected to submit a system description paper to the CHiPSAL-IndoNLP 2027 workshop at COLING 2027. Submitting a paper is not mandatory to participate in the shared task. Papers must follow the workshop submission instructions and will be peer reviewed. Acceptance depends on the quality of the paper, not on the shared task results. All accepted papers will be published in the COLING 2027 workshop proceedings.

## Registration and Proceedings

The registration fee is not required for publication of accepted shared-task papers in the workshop proceedings. Anyone who wishes to attend the workshop, either in person or virtually, must register in accordance with the main conference’s registration policy.

## Timeline

* Start of the competition (Development phase starts; train and eval data released): Nov 20, 2026
* Test phase starts (test data released): Jan 4, 2027
* Test phase ends: Feb 10, 2027
* Shared task paper submission deadline: Feb 20, 2027
* Notification of acceptance: March 20, 2027
* Camera-ready papers due: March 25, 2027

Phase times are in UTC: the Development phase closes on Jan 3, 2027 at 23:59 and the Test phase on Feb 24, 2027 at 23:59.

## Organizers

* Surendrabikram Thapa (Virginia Tech, USA)
* Shuvam Shiwakoti (Virginia Tech, USA)
* Siddhant Bikram Shah (Northeastern University, USA)
* Kritesh Rauniyar (Macquarie University, Australia)
* Surabhi Adhikari (Columbia University, USA)
* Kristina T. Johnson (Northeastern University, USA)
* Kengatharaiyer Sarveswaran (University of Jaffna, Sri Lanka)
* Bal Krishna Bal (Kathmandu University, Nepal)
* Usman Naseem (Macquarie University, Australia)

## Contact

If there are any questions related to the competition, please contact the organizers at ssiwakoti12@gmail.com. Participants in this shared task are encouraged to reach out with any concerns or questions to any of the shared task organizers.

## References

* Thapa, S., Rauniyar, K., Shiwakoti, S., Adhikari, S., Rashid, J., Kim, J., & Naseem, U. (2025). Agentic AI Framework for Low-Resource Essay Evaluation via Scoring, Explanation, and Debate. In *Proceedings of the 2025 IEEE International Conference on Big Data (BigData)*. DOI: [10.1109/BIGDATA66926.2025.11402339](https://doi.org/10.1109/BIGDATA66926.2025.11402339)
