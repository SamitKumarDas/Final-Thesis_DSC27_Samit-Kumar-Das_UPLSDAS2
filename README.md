# Analysis of Medical Scientific Engagement Text Using NLP and Large Language Models

## Overview

This repository contains the code notebooks and analysis outputs for **“Analysis of Medical Scientific Engagement Text Using Natural Language Processing and Large Language Models.”**

The project explores a PubMed-derived biomedical abstract corpus using exploratory data analysis, TF-IDF, topic modelling, sentiment analysis, biomedical sentence embeddings, semantic similarity, and structured interpretation using a local large language model (LLM).

> **Scope:** The dataset contains published PubMed abstracts grouped into three researcher-defined analytical layers. It does not contain direct Medical Science Liaison–healthcare professional engagement transcripts.

## Dataset

The final corpus contains **21,256 unique PubMed records** with these fields:

- `pmid` — PubMed identifier
- `title` — publication title
- `abstract` — abstract text
- `year` — publication year
- `journal` — journal name
- `layer` — researcher-defined analytical layer

| Layer | Records |
|---|---:|
| `L1_scientific_engagement` | 9,599 |
| `L2_safety_risk` | 5,808 |
| `L3_comparative_critical` | 5,849 |
| **Total** | **21,256** |

These layer labels are operational groupings for this study, not universal biomedical categories.

## Repository structure

### Notebooks

| Notebook | Purpose |
|---|---|
| `00_Final_Dataset_Preparation.ipynb` | Prepare the final analysis dataset |
| `01_Dataset_Audit_and_EDA.ipynb` | Audit data quality and inspect corpus characteristics |
| `02_EDA_and_Text_Analysis.ipynb` | Exploratory data analysis and initial text exploration |
| `03_Text_Preprocessing_TFIDF.ipynb` | Text preprocessing and TF-IDF unigram/bigram analysis |
| `04_Topic_Modeling_LDA.ipynb` | Latent Dirichlet Allocation (LDA) topic modelling |
| `05_Sentiment_Analysis.ipynb` | VADER-based lexical sentiment analysis |
| `06_Biomedical_Embeddings_Semantic_Similarity.ipynb` | Generate biomedical sentence embeddings and analyse cosine similarity |
| `07_LLM_Assisted_Interpretation.ipynb` | Generate structured interpretations using a local LLM and review outputs |

### Output folders

- `biomedical_embedding_outputs/` — embeddings, metadata, sampled abstract pairs, and similarity summaries
- `llm_assisted_interpretation_outputs/` — selected sample, raw model outputs/checkpoints, parsed outputs, and manual evaluation files
- `Output images for the thesis/` — figures and visualisations used during analysis and thesis preparation
- `Sentiment_Analysis_outputs/` — sentiment analysis outputs
- `Text_Preprocessing_TFIDF_outputs/` — TF-IDF and preprocessing outputs
- `Topic_Modeling_LDA_outputs/` — LDA model and topic-analysis outputs

Folder names may differ slightly in capitalisation or underscores depending on how they were saved.

## Methods at a glance

1. **Dataset preparation and audit:** validate the corpus and inspect missingness and record counts.
2. **Exploratory analysis:** summarise corpus characteristics and text patterns.
3. **TF-IDF:** identify statistically prominent terms and bigrams.
4. **LDA topic modelling:** identify recurring word co-occurrence patterns and provisionally interpret topics.
5. **VADER sentiment analysis:** calculate lexicon-based polarity scores for abstracts.
6. **Biomedical embeddings:** encode abstracts as 768-dimensional vectors using `pritamdeka/S-PubMedBert-MS-MARCO`.
7. **Semantic similarity:** compare sampled abstracts using cosine similarity. The expanded analysis sampled 10,000 abstracts and analysed 200,000 pairs: 100,000 within-layer and 100,000 between-layer pairs.
8. **Local LLM interpretation:** use `qwen2.5:3b` through Ollama to generate structured outputs for a 100-abstract sample. Ninety-nine outputs were successfully parsed; one request timed out. The available outputs were reviewed using a five-criterion rubric. This is exploratory and is not a validated general measure of model accuracy.

## Important interpretation notes

- The corpus is heavily concentrated in publication year 2025, so it is not suitable for strong long-term publication-trend claims.
- VADER is a general-purpose sentiment tool and is not specifically validated for biomedical scientific abstracts. Its labels should not be interpreted as clinical benefit, harm, or author opinion.
- LDA topic labels are provisional interpretations of model-generated word groups.
- High cosine similarity does not establish scientific agreement, equivalent evidence, or clinical equivalence.
- Pairwise similarity observations can share abstracts and therefore are not all statistically independent.
- Successful JSON parsing does not establish that an LLM response is factually correct.

## Environment and setup

The notebooks were developed in Python/Jupyter on Windows. Exact package versions may vary; check each notebook's import cells for the libraries it requires.

Main tools include:

- Python and Jupyter Notebook/JupyterLab
- pandas and NumPy
- scikit-learn
- Matplotlib and Seaborn
- NLTK / VADER
- sentence-transformers
- PyTorch
- Ollama with `qwen2.5:3b`

### Suggested setup

1. Install Python and Jupyter Notebook or JupyterLab.
2. Install the libraries imported by the notebooks.
3. Put the final dataset file in the location expected by the notebooks, or update the input path in the configuration cell.
4. Run the notebooks in sequence, starting with dataset preparation and audit.
5. For the embedding notebook, install PyTorch and sentence-transformers. GPU acceleration is optional but may reduce processing time.
6. For the LLM notebook, install Ollama, download the model, and ensure the Ollama service is running.

Example Ollama commands:

```bash
ollama pull qwen2.5:3b
ollama run qwen2.5:3b
```

The model name in the notebook must match the model installed locally.

## Expected outputs

Output names may vary by notebook version. The output folders contain artefacts such as:

- cleaned/validated dataset files and audit summaries
- TF-IDF term and n-gram tables
- LDA topic summaries and dominant-topic assignments
- sentiment scores and category summaries
- `abstract_embeddings.npy` and embedding metadata
- sampled similarity pairs and summary tables
- raw and parsed LLM responses, processing checkpoints, and manual evaluation files
- figures and visualisations used in the thesis

Large files, especially the embedding matrix and intermediate CSVs, can make a Git repository large. Consider Git LFS or a separate release/archive for large generated artefacts.

## Reproducibility and responsible use

- Keep random seeds consistent where specified in the notebooks.
- Run notebooks in order when later steps depend on files produced earlier.
- Treat exploratory patterns as descriptive, not causal.
- Retain source abstracts when reviewing generated interpretations.
- Do not upload private, licensed, or restricted data. Check applicable terms and policies before redistributing PubMed-derived material.
- Ensure the repository and its outputs comply with your university's research-integrity, data-use, and AI-use policies. Describe the methods used accurately.

## Citation

If you use or adapt this workflow, cite the associated thesis:

**Das, Samit Kumar.** *Analysis of Medical Scientific Engagement Text Using Natural Language Processing and Large Language Models.* Master's thesis, Liverpool John Moores University.

Add the final submission year and institutional details as required by the thesis title page.

## Author

**Samit Kumar Das**
