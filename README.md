\# Drug ADR Extraction using Transformer-based NLP



Extracting Adverse Drug Reactions (ADRs) from unstructured patient 

reviews using weak supervision, LSTM baseline, and BioBERT NER 

fine-tuning — with SHAP-based explainability.



\## Project structure

\- `notebooks/` — end-to-end pipeline, one notebook per layer

\- `src/` — reusable utility modules

\- `outputs/` — plots, SHAP visualizations, results



\## Pipeline

1\. Data + weak labeling (SIDER keyword matching → BIO tags)

2\. LSTM baseline (binary ADR classification)

3\. BioBERT NER fine-tuning (token-level ADR extraction)

4\. SHAP explainability

5\. Analytics layer



\## Setup

pip install -r requirements.txt



\## Results

(to be filled as project progresses)

```



\---



\*\*Quick check before we move on\*\*



Once you've run through steps 1–5, your folder should look like this when you run `ls -R` (or `tree` if installed):

```

drug-adr-nlp/

├── data/

│   ├── raw/          ← UCI TSV files + meddra\_all\_se.tsv here

│   ├── processed/

│   └── interim/

├── notebooks/        ← empty for now

├── src/

│   ├── \_\_init\_\_.py

│   ├── data\_utils.py

│   ├── label\_utils.py

│   └── train\_utils.py

├── models/

├── outputs/

├── reports/

├── .gitignore

├── requirements.txt

└── README.md


## Results

| Model       | Task                  | F1     |
|-------------|-----------------------|--------|
| LSTM        | Binary classification | 0.723  |
| BioBERT NER | Token classification  | 0.808  |

BioBERT outperforms the LSTM baseline by +8.5 F1 points.
Key improvement: bidirectional context and biomedical pretraining
allow the model to identify multi-word ADR entities that the LSTM
misses due to sequential processing limitations.

Note: Multi-word ADR entities are split at B-ADR boundaries — terms like 'gastrointestinal discomfort' may appear as separate tokens reflecting SIDER's term-level granularity.

Final summary:
  Total reviews analyzed:     30,000
  Reviews with ADR detected:  20,760 (69.2%)
  Unique drugs covered:        2,179
  Unique conditions covered:   622
  Most common ADR term:        pain, Depression, anxiety, nausea


