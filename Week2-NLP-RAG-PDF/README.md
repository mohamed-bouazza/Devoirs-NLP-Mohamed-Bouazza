# Week 2 — RAG sur Documents PDF (Code de la Route)

[![Kaggle](https://img.shields.io/badge/Kaggle-Notebook-blue?logo=kaggle)](https://www.kaggle.com/code/bouazzamohamed/week-2-devoirnlp)
[![Python](https://img.shields.io/badge/Python-3.10-green?logo=python)](https://python.org)

---

## Objectif

Implémenter un système RAG (Retrieval-Augmented Generation) capable d'interroger des documents PDF en langage naturel, appliqué au **Code de la Route marocain**.

---

## Documents de référence utilisés

| Document | Description |
|----------|-------------|
| `code de la route MA52_05.pdf` | Code de la route — règlementation MA |
| `code de la route bo_5874_fr.pdf` | Bulletin Officiel — texte législatif |

---

## Architecture du système

```
[Question utilisateur]
        │
        ▼
[Parsing PDF] ──► [Chunking] ──► [Embeddings]
                                      │
                                      ▼
                               [Index FAISS]
                                      │
                          [Retrieval Top-k chunks]
                                      │
                                      ▼
                          [Prompt enrichi + LLM]
                                      │
                                      ▼
                              [Réponse générée]
```

---

## Contenu du notebook

### 1. Extraction et parsing PDF
- Lecture des PDFs avec `PyMuPDF` (fitz)
- Nettoyage du texte extrait

### 2. Chunking stratégique
- Chunks de 400-500 tokens avec overlap (50 tokens)
- Préservation de la cohérence des paragraphes

### 3. Indexation sémantique
- Encodage avec **Sentence-BERT** (`all-MiniLM-L6-v2`)
- Index vectoriel **FAISS** (IndexFlatIP)

### 4. Retrieval et génération
- Recherche des k chunks les plus pertinents
- Construction du prompt enrichi
- Génération de réponse via LLM

---

## Exemple d'utilisation

```
Question : "Quelle est la vitesse maximale autorisée en agglomération ?"

→ Retrieval : 3 passages pertinents extraits du PDF
→ Réponse   : "La vitesse maximale en agglomération est de 60 km/h,
               conformément à l'article X du code de la route marocain."
```

---

## Technologies utilisées

| Librairie | Usage |
|-----------|-------|
| `PyMuPDF` (fitz) | Extraction texte PDF |
| `sentence-transformers` | Embeddings sémantiques |
| `faiss-cpu` | Index vectoriel |
| `transformers` | LLM pour la génération |

---

## Lien Kaggle

Notebook complet et exécutable :  
**[https://www.kaggle.com/code/bouazzamohamed/week-2-devoirnlp](https://www.kaggle.com/code/bouazzamohamed/week-2-devoirnlp)**

---

*Semaine 2 | Module NLP | M1 MIASD | Enseignante : Ikram Benabdelouahab*
