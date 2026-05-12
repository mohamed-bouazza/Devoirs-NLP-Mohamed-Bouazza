# Week 3 — Système RAG sur le Code de la Route Marocain (Arabe)

[![Kaggle](https://img.shields.io/badge/Kaggle-Notebook-blue?logo=kaggle)](https://www.kaggle.com/code/bouazzamohamed/week3-devoirnlp)
[![Python](https://img.shields.io/badge/Python-3.10-green?logo=python)](https://python.org)
[![GPU](https://img.shields.io/badge/GPU-Tesla%20T4-red?logo=nvidia)](https://www.kaggle.com)

---

## Objectif

Implémenter un système **RAG (Retrieval-Augmented Generation)** sur le dataset structuré du Code de la Route Marocain (`export_final.csv`) pour répondre à des questions juridiques en arabe.

---

## Source de données

| Fichier | Description |
|---------|-------------|
| `export_final.csv` | Dataset issu du Week 2 — 318 articles × 18 colonnes |

---

## Architecture RAG

```
[Question en arabe]
        │
        ▼
[Embedding multilingue]
  intfloat/multilingual-e5-base (768 dims)
        │
        ▼
[Index FAISS — IndexFlatL2]
  463 chunks indexés
        │
        ▼
[Détection hors-domaine]
  Seuil de distance cosinus
        │
        ▼
[Top-k chunks récupérés]
        │
        ▼
[Génération LLM]
  Qwen/Qwen2.5-3B-Instruct
        │
        ▼
[Réponse juridique en arabe]
```

---

## Composants techniques

| Composant | Détail |
|-----------|--------|
| **Modèle d'embedding** | `intfloat/multilingual-e5-base` — 768 dimensions |
| **Index vectoriel** | FAISS `IndexFlatL2` |
| **Chunks indexés** | 463 chunks (issus des 318 articles) |
| **LLM** | `Qwen/Qwen2.5-3B-Instruct` (3B paramètres) |
| **Détection OOD** | Seuil distance cosinus sur score de similarité |

---

## Évaluation du retrieval

### Métriques de précision (k=3 et k=5)

| k | Precision@k | Recall@k | F1@k |
|---|------------|---------|------|
| 3 | 0.095 | — | — |
| **5** | **0.143** | **0.238** | **0.179** |

### Détection hors-domaine (Out-of-Domain)

| Test | Résultat |
|------|---------|
| Questions Code de la Route | Répondu correctement |
| Questions hors-domaine (6 tests) | **6/6 détectées = 100%** |

> Le système refuse correctement de répondre à des questions sans rapport avec le Code de la Route.

---

## Interface utilisateur

**Interface Gradio** en arabe :
- Champ de question en langue arabe
- Affichage des chunks récupérés
- Réponse générée par le LLM
- Indicateur de confiance (in-domain / out-of-domain)

---

## Exemple d'utilisation

```
Question : "ما هي العقوبة في حالة تجاوز السرعة المقررة ؟"

→ Retrieval : 5 articles pertinents récupérés (Art. 68, 69, 70, 71, 304)
→ Réponse   : "يعاقب على تجاوز الحد الأقصى للسرعة بغرامة تتراوح..."
```

---

## Technologies utilisées

| Librairie | Usage |
|-----------|-------|
| `sentence-transformers` | `multilingual-e5-base` embeddings |
| `faiss-cpu` | Index vectoriel FAISS |
| `transformers` | Qwen2.5-3B-Instruct LLM |
| `pandas` | Chargement export_final.csv |
| `gradio` | Interface utilisateur arabe |
| `torch` | Backend GPU Tesla T4 |

---

## Lien Kaggle

Notebook complet et exécutable :  
**[https://www.kaggle.com/code/bouazzamohamed/week3-devoirnlp](https://www.kaggle.com/code/bouazzamohamed/week3-devoirnlp)**

---

*Semaine 3 | Module NLP | M1 MIASD | Enseignante : Ikram Benabdelouahab*
