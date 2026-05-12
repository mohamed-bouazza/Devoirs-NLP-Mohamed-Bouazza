# Week 1 — Pipeline NLP : Prétraitement & Analyse de Texte

[![Kaggle](https://img.shields.io/badge/Kaggle-Notebook-blue?logo=kaggle)](https://www.kaggle.com/code/bouazzamohamed/week-1-devoirnlp)
[![Python](https://img.shields.io/badge/Python-3.10-green?logo=python)](https://python.org)

---

## Objectif

Construire un pipeline NLP complet pour le prétraitement, l'analyse et la représentation de textes en langage naturel.

---

## Contenu du notebook

### 1. Prétraitement du texte
- Tokenisation (mot, phrase, sous-mot)
- Suppression des stop words
- Stemming (PorterStemmer) et Lemmatisation (WordNet)
- Normalisation : minuscules, ponctuation, caractères spéciaux

### 2. Représentations vectorielles
- **Bag of Words (BoW)** — matrice terme-document
- **TF-IDF** — pondération par fréquence inverse
- **Word2Vec** — embeddings denses (Skip-gram / CBOW)
- **Sentence-BERT** — embeddings contextuels

### 3. Analyse linguistique
- POS Tagging (étiquetage morpho-syntaxique)
- Named Entity Recognition (NER)
- Analyse de sentiment

### 4. Visualisations
- Nuage de mots (WordCloud)
- Distribution des fréquences
- Projection 2D des embeddings (PCA / t-SNE)

---

## Technologies utilisées

| Librairie | Usage |
|-----------|-------|
| `nltk` | Tokenisation, stop words, stemming |
| `spacy` | Lemmatisation, POS, NER |
| `scikit-learn` | TF-IDF, BoW |
| `gensim` | Word2Vec |
| `sentence-transformers` | Sentence-BERT |
| `matplotlib` / `seaborn` | Visualisations |

---

## Lien Kaggle

Notebook complet et exécutable :  
**[https://www.kaggle.com/code/bouazzamohamed/week-1-devoirnlp](https://www.kaggle.com/code/bouazzamohamed/week-1-devoirnlp)**

---

*Semaine 1 | Module NLP | M1 MIASD | Enseignante : Ikram Benabdelouahab*
