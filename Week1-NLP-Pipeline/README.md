# Week 1 — Pipeline NLP : Prétraitement & Analyse de Texte (Français)

[![Kaggle](https://img.shields.io/badge/Kaggle-Notebook-blue?logo=kaggle)](https://www.kaggle.com/code/bouazzamohamed/week-1-devoirnlp)
[![Python](https://img.shields.io/badge/Python-3.10-green?logo=python)](https://python.org)
[![spaCy](https://img.shields.io/badge/spaCy-fr__core__news__sm-purple)](https://spacy.io)

---

## Objectif

Construire un pipeline NLP complet en Python avec **spaCy** (`fr_core_news_sm`) sur des textes français, puis appliquer ce pipeline sur des textes arabes et un document PDF.

---

## Architecture du pipeline

```
[Texte brut]
     │
     ▼
[Collecte / Lecture PDF]
     │
     ▼
[Prétraitement]
  ├── Mise en minuscules
  ├── Suppression ponctuation & chiffres
  └── Suppression stop words (spaCy fr)
     │
     ▼
[Analyse linguistique]
  ├── Tokenisation
  ├── POS Tagging (Part-of-Speech)
  └── NER (Named Entity Recognition)
     │
     ▼
[Vectorisation TF-IDF]
     │
     ▼
[Résultats & Visualisation]
```

---

## Exemples traités

### Exemple 1 — Pipeline complet sur texte d'actualité

**Phrase testée :**
```
"Apple fondée par Steve Jobs en Californie"
```

**Résultat NER (spaCy fr_core_news_sm) :**
| Entité | Type |
|--------|------|
| Apple | ORG |
| Steve Jobs | PER |
| Californie | LOC |

---

### Exemple 2 — TF-IDF sur phrase académique FST Tanger

**Fonction utilisée :**
```python
trace_nlp_pipeline("Les ingénieurs étudient les algorithmes d'IA à la FST de Tanger!")
```

**Scores TF-IDF obtenus :**
| Token lemmatisé | Score TF-IDF |
|----------------|-------------|
| étudier | 0.48 |
| ingénieur | 0.48 |
| algorithme | 0.37 |
| ia | 0.37 |
| tanger | 0.37 |

---

### Exemple 3 — Stemming vs Lemmatisation

Comparaison entre **SnowballStemmer** (règles morphologiques) et **Lemmatisation spaCy** (formes canoniques) sur des verbes et noms français.

---

## Devoir — Extension sur textes arabes + PDF

Le devoir applique le même pipeline à :
- **Textes en arabe** (au lieu du français)
- **Extraction depuis un PDF** via `PyPDF2`

---

## Technologies utilisées

| Librairie | Usage |
|-----------|-------|
| `spacy` + `fr_core_news_sm` | Tokenisation, POS, NER, Lemmatisation |
| `nltk` | Stop words, SnowballStemmer |
| `scikit-learn` | TF-IDF Vectorizer |
| `PyPDF2` | Extraction de texte depuis PDF |
| `matplotlib` | Visualisations |

---

## Lien Kaggle

Notebook complet et exécutable :  
**[https://www.kaggle.com/code/bouazzamohamed/week-1-devoirnlp](https://www.kaggle.com/code/bouazzamohamed/week-1-devoirnlp)**

---

*Semaine 1 | Module NLP | M1 MIASD | Enseignante : Ikram Benabdelouahab*
