# Week 4 — Devoir 3 : 7 Architectures RAG pour la Génération de Règles SNORT

[![Kaggle](https://img.shields.io/badge/Kaggle-Notebook-blue?logo=kaggle)](https://www.kaggle.com/code/bouazzamohamed/week-4-devoirnlp)
[![Python](https://img.shields.io/badge/Python-3.10-green?logo=python)](https://python.org)
[![GPU](https://img.shields.io/badge/GPU-Tesla%20T4-red?logo=nvidia)](https://www.kaggle.com)

---

## Objectif

Implémenter, comparer et évaluer **7 architectures RAG** appliquées à la génération de règles SNORT (IDS) à partir de descriptions en langage naturel de comportements réseau suspects.

---

## Dataset

- **Source :** Emerging Threats Open Rules (ETOpen)
- **Taille :** 500 règles SNORT (sampling stratifié)
- **Catégories :** 24 classtypes (web-application-attack, trojan-activity, attempted-recon…)

---

## Modèles utilisés

| Rôle | Modèle | Paramètres |
|------|--------|------------|
| LLM | `Qwen2.5-7B-Instruct` | 7B (4-bit NF4 quantization) |
| Embedder | `BAAI/bge-small-en-v1.5` | 384 dimensions |
| Reranker | `cross-encoder/ms-marco-MiniLM-L-6-v2` | Cross-encoder |
| Sparse | `BM25Okapi` | Tokenizer cybersécurité |

---

## Les 7 Architectures comparées

| # | Architecture | Principe |
|---|-------------|----------|
| 1 | **Baseline** | LLM seul, sans contexte RAG |
| 2 | **Classic RAG** | Dense retrieval FAISS → LLM |
| 3 | **Re-ranking RAG** | Dense → Cross-encoder reranker → LLM |
| 4 | **Hybrid RAG** | Dense + BM25 fusionnés (RRF) → LLM |
| 5 | **Multi-hop RAG** | Recherche itérative multi-étapes |
| 6 | **Graph RAG** | Graphe de connaissances NetworkX |
| 7 | **Agentic RAG** | Pattern ReAct : décision autonome de retrieval |

---

## Résultats — Quality Score par architecture

| Architecture | Latence | Quality/10 | Syntax% | Hallucinations |
|-------------|---------|-----------|---------|----------------|
| **rag_classic** | 20.2s | **8.17** ← meilleur | 83% | 0 |
| rag_hybrid | 23.3s | 8.00 | 83% | 0 |
| graph_rag | 17.3s | 7.67 | 83% | 0 |
| multi_hop | 25.3s | 7.17 | 66% | 0 |
| rag_rerank | 24.0s | 7.17 | 66% | 0 |
| agentic_rag | 25.4s | 6.50 | 83% | 1 |
| **baseline** | 6.6s | 5.33 ← référence | 100%* | 0 |

> *La syntaxe baseline à 100% est trompeuse : les règles générées sont trop génériques (`any any -> any any`). Le **Quality Score** révèle la vraie valeur ajoutée du RAG.

---

## Métriques d'évaluation SNORT

| Métrique | Description | Plage |
|----------|-------------|-------|
| **Quality Score** | Richesse de détection (flow, content, pcre, classtype…) | 0 – 10 |
| **Syntax Valid %** | Structure minimale correcte | 0 – 100% |
| **Truncation Rate** | Règles coupées avant `;)` | 0 – 100% |
| **Hallucination Rate** | SIDs invalides ou CVEs malformés | 0 – 100% |

## Métriques de retrieval (Dense FAISS, k=3)

| Méthode | P@3 | R@3 | MRR |
|---------|-----|-----|-----|
| Dense (FAISS) | 0.533 | 0.500 | 0.533 |
| Hybrid (RRF) | 0.400 | 0.300 | 0.500 |

---

## Queries de test (6 queries diversifiées)

```
1. Detect TCP port scanning on web server
2. Generate rule for CVE-2021-44228 Log4Shell JNDI exploitation
3. Detect SQL injection with UNION SELECT pattern
4. Detect ransomware after RDP brute force initial access
5. Detect reconnaissance and exploitation against Apache servers
6. Detect sophisticated APT command and control beaconing
```

---

## Livrables

- `snort_dataset.json` — Dataset de 500 règles SNORT structurées
- `rag_results.json` — Résultats complets des 7 architectures sur 6 queries
- `metrics.csv` — Tableau de benchmarking comparatif
- `tsne_snort.png` — Visualisation t-SNE des embeddings SNORT
- Interface Gradio interactive (Quality: 9/10)

---

## Conclusion

> Le RAG améliore significativement la qualité des règles SNORT générées.  
> L'architecture **Classic RAG** obtient le meilleur score (8.17/10).  
> L'architecture **Hybrid RAG** (dense + BM25) est la plus robuste pour la cybersécurité car elle capture les identifiants exacts (CVE, ports, protocoles) grâce à la recherche sparse BM25.

---

## Lien Kaggle

Notebook complet et exécutable :  
**[https://www.kaggle.com/code/bouazzamohamed/week-4-devoirnlp](https://www.kaggle.com/code/bouazzamohamed/week-4-devoirnlp)**

---

*Semaine 4 | Devoir 3 | Module NLP | M1 MIASD | Enseignante : Ikram Benabdelouahab*
