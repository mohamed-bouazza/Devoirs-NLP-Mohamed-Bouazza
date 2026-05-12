# Week 3 — Devoir 2 : Comparaison des 7 Architectures RAG

[![Kaggle](https://img.shields.io/badge/Kaggle-Notebook-blue?logo=kaggle)](https://www.kaggle.com/code/bouazzamohamed/week3-devoirnlp)
[![Python](https://img.shields.io/badge/Python-3.10-green?logo=python)](https://python.org)
[![GPU](https://img.shields.io/badge/GPU-Tesla%20T4-red?logo=nvidia)](https://www.kaggle.com)

---

## Objectif

Implémenter et comparer **7 architectures RAG** appliquées à la génération de règles SNORT depuis des descriptions en langage naturel.

---

## Dataset SNORT

- **Source :** Emerging Threats Open Rules (ETOpen)
- **Taille :** 500 règles (sampling stratifié, 24 classtypes)
- **Top classtypes :** web-application-attack, trojan-activity, attempted-recon...

---

## Les 7 Architectures

| # | Architecture | Principe |
|---|-------------|----------|
| 1 | **Baseline** | LLM seul, sans contexte |
| 2 | **Classic RAG** | Dense retrieval FAISS → LLM |
| 3 | **Re-ranking RAG** | Dense → Cross-encoder → LLM |
| 4 | **Hybrid RAG** | Dense + BM25 fusionnés (RRF) → LLM |
| 5 | **Multi-hop RAG** | Recherche itérative multi-étapes |
| 6 | **Graph RAG** | Graphe de connaissances NetworkX |
| 7 | **Agentic RAG** | Pattern ReAct : décision autonome |

---

## Modèles utilisés

| Rôle | Modèle |
|------|--------|
| LLM | `Qwen2.5-7B-Instruct` (4-bit) |
| Embedder | `BAAI/bge-small-en-v1.5` |
| Reranker | `cross-encoder/ms-marco-MiniLM-L-6-v2` |
| Sparse | `BM25Okapi` |

---

## Résultats

| Architecture | Latence | Quality/10 | Syntax% | Halluc. |
|-------------|---------|-----------|---------|---------|
| **rag_classic** | 20.2s | **8.17** | 83% | 0 |
| **rag_hybrid** | 23.3s | 8.00 | 83% | 0 |
| graph_rag | 17.3s | 7.67 | 83% | 0 |
| multi_hop | 25.3s | 7.17 | 66% | 0 |
| rag_rerank | 24.0s | 7.17 | 66% | 0 |
| agentic_rag | 25.4s | 6.50 | 83% | 1 |
| baseline | 6.6s | 5.33 | 100% | 0 |

> **Conclusion :** `rag_classic` obtient le meilleur Quality Score (8.17/10). `rag_hybrid` est le plus robuste pour la cybersécurité (CVEs, ports exacts capturés par BM25).

---

## Retrieval Benchmarking (k=3)

| Méthode | P@3 | R@3 | MRR |
|---------|-----|-----|-----|
| Dense (FAISS) | 0.533 | 0.500 | 0.533 |
| Hybrid (RRF) | 0.400 | 0.300 | 0.500 |

---

## Livrables

- `snort_dataset.json` — 500 règles parsées
- `rag_results.json` — outputs des 7 architectures
- `metrics.csv` — tableau comparatif
- `tsne_snort.png` — visualisation t-SNE
- Interface **Gradio** interactive

---

## Lien Kaggle

**[https://www.kaggle.com/code/bouazzamohamed/week3-devoirnlp](https://www.kaggle.com/code/bouazzamohamed/week3-devoirnlp)**

---

*Semaine 3 | Devoir 2 | Module NLP | M1 MIASD | Enseignante : Ikram Benabdelouahab*
