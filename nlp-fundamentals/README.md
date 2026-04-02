# NLP Fundamentals — Demo Notebook

Companion interactive demo for the NLP Fundamentals seminar slide deck.

## Quick Start

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/behitek/talks/blob/main/nlp-fundamentals/nlp-fundamentals-demo.ipynb) [![View slides](https://img.shields.io/badge/View-Slides-blue)](https://behitek.github.io/talks/nlp-fundamentals/)

## Before the Session (Presenter Only)

1. Open the notebook in Colab.
2. Run **all cells in the SETUP section** before the audience arrives (takes ~3–5 minutes for model downloads).
3. Confirm both ✅ messages appear (BERT tokenizer loaded, word2vec loaded).
4. Also **pre-run the UMAP cell** (Part 3) during setup — do not re-run it live as the layout is non-deterministic.
5. Collapse the SETUP section so only the PART headers are visible.

## During the Session

- Use Colab's **table of contents sidebar** (☰ icon, left panel) to jump between PART 1, PART 2, PART 3.
- In **PART 2 — Similarity**, invite the audience to suggest a word. Edit `query_word = "king"` and re-run the cell.
- **Do not re-run the UMAP cell live** — the layout is non-deterministic. Keep the pre-run output visible.

## Notebook Sections

| Section | Slides it supports | What it shows |
|---|---|---|
| SETUP | Run before session | pip install, BERT + word2vec loading |
| PART 1 — Tokenization | Section 2.1, 2.3 | BPE chips for "river bank" vs "bank account", different IDs |
| PART 2 — Similarity | Section 2.2 | Top similar words for any query + king−man+woman analogy |
| PART 3 — Embedding Map | Section 2.2 | UMAP 2D plot of 40 curated words in 5 semantic clusters |
| Closing Callback | Section 4 | Resolution of the opening bank puzzle |

## Package Versions (tested)

```
transformers>=4.38.0
torch>=2.0.0
gensim>=4.3.0
umap-learn>=0.5.6
matplotlib>=3.8.0
numpy>=1.24.0
```

All packages except `umap-learn` are pre-installed on Colab. The SETUP cell handles installation automatically.
