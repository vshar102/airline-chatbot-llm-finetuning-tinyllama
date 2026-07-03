# Airline Chatbot — LLM Fine-Tuning with TinyLlama (LoRA/PEFT)

`airline-chatbot-llm-finetuning-tinyllama`  ·  Portfolio project  ·  MIT License

## Overview

Fine-tunes a TinyLlama causal language model so it can classify a customer's intent (e.g. booking a flight, checking baggage status, requesting special assistance) from a free-text airline support message and generate a helpful response.

## Problem Statement

Support teams accumulate large volumes of labeled chat transcripts but rarely turn that data into a working assistant. This project takes a labeled airline customer-service chat dataset and turns it into a fine-tuned small language model that can be deployed as a first-line support assistant.

## Approach

Uses Hugging Face `transformers` + `peft` (LoRA) to parameter-efficiently fine-tune TinyLlama on a reduced, intent-balanced subset of a travel-query dataset, rather than full fine-tuning (which would be far more expensive for a 1B-scale model). `trl` is used for the fine-tuning loop.

## Tech Stack

Python, PyTorch, Hugging Face Transformers, PEFT (LoRA), TRL, Datasets

## Results

The fine-tuned model produces intent predictions and generated responses for held-out airline support queries. See the notebook's evaluation cells for qualitative examples; a quantitative accuracy/loss curve is included inline.

## Setup

```bash
python -m venv .venv && source .venv/bin/activate
pip install torch transformers peft trl datasets jupyter
```
The airline chat dataset is not included in this repository (see .gitignore) — the notebook downloads/loads it into `data/` on first run.

## Usage

```bash
jupyter notebook notebook.ipynb
```
Run all cells top-to-bottom. GPU strongly recommended; on CPU-only machines, reduce the training subset size further.

## Project Structure

```
.
├── notebook.ipynb        # fine-tuning + evaluation
├── data/                 # (git-ignored) training data, populated by the notebook
└── README.md
```

## Security Considerations

No API keys or credentials are committed to this repository. Where the project
calls an external API, copy `.env.example` to `.env` and supply your own key —
`.env` is git-ignored.

## Troubleshooting

- If a notebook cell fails on a missing package, install the pinned versions
  in `requirements.txt` (or the imports listed in Tech Stack above) rather than
  the latest release, since some ML libraries change APIs between minor versions.
- Large datasets and model checkpoints are intentionally excluded from this
  repository (see `.gitignore`) to keep it lightweight — see Setup for how to
  obtain or regenerate them.

## Roadmap

- [ ] Add a `requirements.txt` with pinned versions
- [ ] Package inference as a small CLI/API instead of notebook-only
- [ ] Add automated evaluation metrics (BLEU/ROUGE or intent-accuracy) tracked over training runs

## License

Licensed under the MIT License — see `LICENSE`.

---
*This project originated as a guided DataCamp practical exercise and was
independently re-packaged, documented, and prepared for portfolio presentation.
The premise/business framing in the notebook is illustrative, not a real client engagement.*
