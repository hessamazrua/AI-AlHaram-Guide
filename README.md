# AlHaram Guide: AI-Powered Smart Kiosk for Pilgrims

CS316 Course Project | Semester 252 | Prince Sultan University
Supervised by: Dr. Souad Larabi-Marie-Sainte

---

## Project Overview

AlHaram Guide is an AI-powered smart touchscreen kiosk designed to assist pilgrims performing Hajj and Umrah at the Grand Mosque in Mecca. The system provides real-time, multilingual guidance to help pilgrims navigate, perform rituals, and access services — reducing reliance on human guides and improving the overall experience.

Key features:
- Multilingual support: Arabic, English, Urdu, Turkish, French, Malayalam, Bengali
- Interactive navigation maps with shortest-route detection
- Step-by-step Hajj and Umrah ritual guidance
- AI-powered smart assistant with automatic language detection
- Emergency contacts and safety guidance
- Prayer times and religious information
- Analytics dashboard for system usage insights

---

## Team Members

| Name | Role |
|------|------|
| Hessa Almazrua | Project Manager and Research |
| Aljoharah Alsaeegh | Data and AI Expert |
| Najd Alluhidan | Front-end Developer |
| Aldanah Aldehaim | Backend Developer |
| Tib Othman | Backend Developer |

---

## Project Structure

```
AlHaram_Guide/
├── AlHaram_Guide.ipynb              # Main notebook — EDA + ML models
├── Responses.csv                    # Primary survey dataset (39 participants)
├── synthetic_interactions.csv       # Synthetic dataset (10,000 records)
└── README.md                        # This file
```

---

## Datasets

### 1. Primary Survey Dataset (Responses.csv)
- Size: 39 real participants
- Source: Online survey conducted by the team (January 2026)
- Content: Pilgrim challenges, feature preferences, kiosk acceptance, language barriers
- Privacy: Fully anonymized — no personal identifiers collected

### 2. Synthetic Interaction Dataset (synthetic_interactions.csv)
- Size: 10,000 simulated pilgrim interactions
- Generated using: Python Faker library
- Fields: interaction_id, timestamp, hour, language, query_type, location, age_group, session_duration_sec, response_time_sec, satisfaction
- Purpose: User behavior modeling, system load analysis, ML model training and evaluation

---

## How to Run

### Requirements

```bash
pip install pandas numpy matplotlib seaborn faker jupyter scikit-learn langdetect scipy
```

### Steps

1. Clone the repository:
```bash
git clone https://github.com/ba443/AlHaram-Guide.git
cd AlHaram-Guide
```

2. Place Responses.csv in the same directory as the notebook.

3. Launch Jupyter:
```bash
jupyter notebook AlHaram_Guide.ipynb
```

4. Run all cells. Charts save automatically to output/

---

## Notebook Structure

| Section | Content |
|---------|---------|
| 1 | Imports and configuration |
| 2 | Data loading and preprocessing |
| 3 | Survey data analysis (Figures 1-6) |
| 4 | Synthetic dataset generation |
| 5 | Synthetic dataset analysis (Figures 7-11) |
| 6 | Descriptive statistics summary |
| 7 | Key findings |
| 8 | Language detection model — ANR |
| 9 | Query type classifier — NLP component |
| 10 | Memory optimization documentation (Appendix) |

---

## ML Models

### Language Detection (ANR)
- Library: langdetect
- Algorithm: Bayesian classifier on n-gram character models
- Languages supported: 55 (7 targeted for this system)
- Target accuracy: 85%
- Evaluated against a labeled test set of multilingual pilgrim queries

### Query Type Classifier (NLP Component)
Three models trained and compared using TF-IDF vectorization (unigrams + bigrams, max 5,000 features):

| Model | Description |
|-------|-------------|
| Logistic Regression | Primary model — interpretable, probability outputs for confidence thresholding |
| Random Forest | Ensemble baseline |
| Linear SVM | Strong linear classifier for text |

Evaluation metrics: Accuracy, F1 (weighted), Precision, Recall, 5-Fold Cross-Validation.

Classes: Ritual Guidance, Navigation/Maps, Prayer Times, Emergency Assistance, General Information, Zamzam Location.

Note: The paper proposes a full RAG system (embedding + retrieval + generation) as the production NLP architecture. The TF-IDF classifier implemented here serves as the supervised ML component required for model training and evaluation. RAG is proposed as a future extension.

---

## Memory Optimization (Appendix)

Documented in Section 10 of the notebook:

- TF-IDF produces a sparse matrix (scipy.sparse.csr_matrix) instead of a dense array, reducing memory usage by over 90% at scale
- Categorical dtypes applied to low-cardinality string columns (language, query_type, location, age_group)
- int8 dtype used for small integer columns (hour, satisfaction)
- Lazy loading with nrows parameter during data exploration
- Sklearn Pipeline used to avoid redundant matrix recomputation across train/test splits

---

## Ethical Considerations

- No biometric data collected
- All survey data fully anonymized
- Compliant with Saudi personal data protection regulations
- Content aligned with Islamic values and cultural sensitivities
- System designed for accessibility: elderly users, people with disabilities, non-Arabic speakers

---

## References

- Ministry of Hajj and Umrah. (2023). Hajj and Umrah services and guidelines. Kingdom of Saudi Arabia.
- OpenStreetMap contributors. (2024). Open geographic data.
- Shah, A. A. (2025). A machine learning model for crowd density classification in Hajj video frames. arXiv:2501.04911.
- Alzahrani, R., & Algethami, N. (2025). Leveraging machine learning for optimal pilgrim crowd management. Electronics, 14(13), 2507.
- Khan, E. A., & Shambour, M. K. (2025). AI applications in mega events: Hajj and Umrah as a case study. Global Journal of Economics and Business, 15(3), 375-382.
