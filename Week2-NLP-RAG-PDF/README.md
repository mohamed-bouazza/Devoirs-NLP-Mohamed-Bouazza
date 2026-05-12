# Week 2 — Pipeline NLP Arabe : Code de la Route Marocain (Loi 52-05)

[![Kaggle](https://img.shields.io/badge/Kaggle-Notebook-blue?logo=kaggle)](https://www.kaggle.com/code/bouazzamohamed/week-2-devoirnlp)
[![Python](https://img.shields.io/badge/Python-3.10-green?logo=python)](https://python.org)
[![Arabic NLP](https://img.shields.io/badge/NLP-Arabic-green)](https://pyarabic.readthedocs.io)

---

## Objectif

Construire un pipeline NLP complet sur un document juridique arabe : le **Code de la Route Marocain (Loi 52-05)**, depuis l'extraction PDF jusqu'à la classification automatique et l'export structuré.

---

## Document source

| Document | Description |
|----------|-------------|
| `code de la route MA52_05.pdf` | Loi n°52-05 — Code de la Route du Maroc |

**Statistiques d'extraction :**
- **318 articles** extraits
- **216 951 caractères** de texte arabe

---

## Pipeline complet

### 1. Extraction PDF
- Lecture avec `pypdf` (`PdfReader`)
- Extraction de tout le texte arabe brut

### 2. Normalisation du texte arabe (`pyarabic`)
| Opération | Description |
|-----------|-------------|
| Suppression tashkeel | Retrait des voyelles courtes (حركات) |
| Normalisation hamza | Uniformisation des formes de ء / أ / إ / آ |
| Normalisation ta marbuta | ة → ه |
| Suppression BIDI chars | Retrait des caractères de direction Unicode |

### 3. Segmentation par articles
- **Regex** pour détecter les patterns `المادة X` et `الفصل X`
- **318 articles** segmentés et structurés

### 4. Extraction d'informations juridiques (Regex)
| Champ extrait | Exemple / Valeur max |
|--------------|----------------------|
| `amende_max` | jusqu'à **500 000 DH** (Art. 304) |
| `points_retrait` | jusqu'à 4 points |
| `categories_permis` | A ; A1 ; AM ; B ; C ; D ; E(B) ; E(C) ; E(D) |
| `type_paragraphe` | sanction (30%), obligation (27%), définition... |

### 5. Clustering non supervisé
- **TF-IDF** (3 000 features, stop words arabes)
- **KMeans** — 8 clusters thématiques
  - Cluster 0 : Infractions et sanctions
  - Cluster 1 : Permis de conduire
  - Cluster 2 : Signalisation routière
  - ...

### 6. Classification supervisée
| Modèle | Accuracy |
|--------|----------|
| Naive Bayes | 0.500 |
| Logistic Regression | 0.582 |
| **SVM Linear** | **0.623** ← meilleur |

---

## Export final

`export_final.csv` — **318 lignes × 18 colonnes** :

| Colonne | Description |
|---------|-------------|
| `article_num` | Numéro de l'article |
| `texte_original` | Texte arabe brut |
| `texte_normalise` | Texte après normalisation pyarabic |
| `amende_max` | Montant max de l'amende (DH) |
| `points_retrait` | Points de permis retirés |
| `categories_permis` | Catégories de permis concernées |
| `type_paragraphe` | sanction / obligation / définition... |
| `cluster_kmeans` | Cluster KMeans (0-7) |
| `classe_supervisee` | Label de classification SVM |
| ... | 9 autres colonnes structurées |

---

## Technologies utilisées

| Librairie | Usage |
|-----------|-------|
| `pypdf` | Extraction texte PDF arabe |
| `pyarabic` | Normalisation texte arabe |
| `scikit-learn` | TF-IDF, KMeans, SVM, Naive Bayes, LogReg |
| `re` (regex) | Segmentation articles, extraction amendes/permis |
| `pandas` | Structuration et export CSV |
| `matplotlib` / `seaborn` | Visualisations clusters |

---

## Lien Kaggle

Notebook complet et exécutable :  
**[https://www.kaggle.com/code/bouazzamohamed/week-2-devoirnlp](https://www.kaggle.com/code/bouazzamohamed/week-2-devoirnlp)**

---

*Semaine 2 | Module NLP | M1 MIASD | Enseignante : Ikram Benabdelouahab*
