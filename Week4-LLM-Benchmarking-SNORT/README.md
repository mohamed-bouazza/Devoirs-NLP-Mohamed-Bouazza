# Week 4 — Devoir 3 : Comparaison des LLMs & Métriques d'Évaluation SNORT

[![Kaggle](https://img.shields.io/badge/Kaggle-Notebook-blue?logo=kaggle)](https://www.kaggle.com/code/bouazzamohamed/week-4-devoirnlp)
[![Python](https://img.shields.io/badge/Python-3.10-green?logo=python)](https://python.org)
[![GPU](https://img.shields.io/badge/GPU-Tesla%20T4-red?logo=nvidia)](https://www.kaggle.com)

---

## Objectif

Benchmarker plusieurs LLMs sur la génération de règles SNORT et implémenter des métriques d'évaluation avancées pour mesurer objectivement la qualité des sorties.

---

## LLMs comparés

| Modèle | Paramètres | Quantization | VRAM |
|--------|-----------|--------------|------|
| `Qwen2.5-7B-Instruct` | 7B | 4-bit NF4 | ~5 GB |
| `Mistral-7B-Instruct` | 7B | 4-bit NF4 | ~5 GB |
| `LLaMA-3.1-8B-Instruct` | 8B | 4-bit NF4 | ~6 GB |

---

## Métriques implémentées

### Qualité SNORT (spécifiques au projet)

| Métrique | Description | Plage |
|----------|-------------|-------|
| **Quality Score** | 10 critères de richesse (flow, content, pcre, classtype...) | 0 – 10 |
| **Syntax Valid %** | Structure minimale correcte | 0 – 100% |
| **Truncation Rate** | Règles coupées avant `;)` | 0 – 100% |
| **Hallucination Rate** | SIDs invalides ou CVEs malformés | 0 – 100% |

### Génération standard

| Métrique | Description |
|----------|-------------|
| **BLEU Score** | Similarité n-grammes avec règles de référence |
| **ROUGE-L** | Rappel de la sous-séquence commune |
| **Latency (s)** | Temps de génération par règle |
| **Token/s** | Débit de génération |

### Retrieval

| Métrique | Description |
|----------|-------------|
| **Precision@k** | Fraction de docs pertinents parmi les k récupérés |
| **Recall@k** | Fraction de docs pertinents récupérés |
| **MRR** | Mean Reciprocal Rank |
| **NDCG@k** | Normalized Discounted Cumulative Gain |

---

## Queries de test

```
1. Detect TCP port scanning on web server
2. Generate rule for CVE-2021-44228 Log4Shell JNDI exploitation
3. Detect SQL injection with UNION SELECT pattern
4. Detect ransomware after RDP brute force initial access
5. Detect reconnaissance and exploitation against Apache servers
6. Detect sophisticated APT command and control beaconing
```

---

## Résultats clés

```
Architecture    Quality/10   Latence   Truncated   Halluc.
rag_classic       8.17       20.2s      0/6          0     ← MEILLEUR
rag_hybrid        8.00       23.3s      1/6          0
graph_rag         7.67       17.3s      1/6          0
multi_hop         7.17       25.3s      3/6          0
rag_rerank        7.17       24.0s      2/6          0
agentic_rag       6.50       25.4s      1/6          1
baseline          5.33        6.6s      1/6          0     ← RÉFÉRENCE
```

### Exemple de règle générée (Quality: 9/10)

```snort
alert tcp $EXTERNAL_NET any -> $HTTP_SERVERS $HTTP_PORTS
(msg:"ET SCAN TCP Port Scanning on Web Server";
 flow:to_server,established;
 content:"GET"; http_method;
 content:"HTTP/1.1 404 Not Found"; http_status;
 content:"User-Agent"; http_header;
 classtype:portscan; sid:2008500; rev:1;
 metadata:created_at 2010_07_30, confidence High;)
```

---

## Livrables

- `snort_dataset.json` — 500 règles SNORT structurées
- `rag_results.json` — résultats complets des 7 architectures
- `metrics.csv` — tableau de benchmarking
- `tsne_snort.png` — visualisation t-SNE
- Interface **Gradio** déployée (Quality: 9/10 | Complete)

---

## Lien Kaggle

**[https://www.kaggle.com/code/bouazzamohamed/week-4-devoirnlp](https://www.kaggle.com/code/bouazzamohamed/week-4-devoirnlp)**

---

*Semaine 4 | Devoir 3 | Module NLP | M1 MIASD | Enseignante : Ikram Benabdelouahab*
