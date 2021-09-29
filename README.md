# Modeling Hospital Readmissions

The goal of this project is to build a predictive model for 30-day readmission based on the Medical Information Mart for Intensive Care (MIMIC III v1.4) database. The set contains admissions for intensive care unit (ICU) patients.

To model the patient readmission we use the ADMISSIONS and NOTEEVENTS tables:

- ADMISSIONS contains every unique hospitalization for each patient in the database
- NOTEEVENTS contains the deidentified notes, including nursing and physician notes, ECG reports, imaging reports, and discharge summaries.



## Data

In this project we use the MIMIC-III database (available here: [https://physionet.org](https://physionet.org))

- The instuctions of how to get an access to the database are [here](https://mimic.mit.edu/docs/gettingstarted/).

- The detailed overview of the MIMIC-III data is provided [here](https://mimic.mit.edu/docs/iii/tables/).

## Data preprocessing 

See `notebooks/preprocess-data.ipynb`


## Modeling
BOW XGBoost baseline model: `notebooks/model-BOW-XGBoost.ipynb`

## TO DO
Things to improve:

- Try BERT/ClinicalBERT, the problem is it has max number of input tokens=512, we would need to split the text into chunks, and classify each chunk separately, then combine the results together (using the majority class etc.)
- Try [Longformer](https://huggingface.co/transformers/model_doc/longformer.html) which has an attention mechanism that scales linearly with sequence length, making it easy to process documents of thousands of tokens or longer.
- Try [Reformer](https://huggingface.co/transformers/model_doc/reformer.html)
- See this paper: [LONG RANGE ARENA: A BENCHMARK FOR EFFICIENT TRANSFORMERS](https://arxiv.org/pdf/2011.04006.pdf)
- For simplicity, we used the the discharge summary, but we could use all the notes by concatenating.
- There are cases with multiple discharge summarie per hospital admission, we use the last one (minor improv).
- Use ensembling with other available data.
- Try oversampling the positives, generate synthetic data (SMOTE etc).


## References

[1] Predicting readmission risk from doctors’ notes, E.Craig et al (2017) [PDF](https://arxiv.org/pdf/1711.10663.pdf)

[2] ClinicalBERT: Modeling Clinical Notes and Predicting Hospital Readmission, K.Huang, et al. (2020) [PDF](https://arxiv.org/pdf/1904.05342v3.pdf)

[3] Publicly Available Clinical BERT Embeddings, E.Alsentzer et al. (2019) [PDF](https://aclanthology.org/W19-1909.pdf)

[4] https://github.com/andrewwlong/mimic_bow

