# Detecting the Language of Greenwashing: Specificity Classification of Climate Disclosures

Course project for **Advanced Natural Language Processing**, Barcelona School of Economics (BSE), June 2026.

Authors: Cameron Armour, Marco Canal, Michael Duarte Gonçalves, Mircea-Adrian Guinea.

The notebook classifies climate-related sentences as **specific** or **non-specific**, a linguistic signal that helps separate substantive sustainability claims from vague ones. It compares rule-based, fine-tuned transformer, zero-shot, few-shot and LLM-augmented approaches on the `climatebert/climate_specificity` dataset, then studies the label-noise ceiling and model compression.

## Repository layout

```
.
├── notebooks/
│   └── Armour_Canal_Goncalves_Guinea_Climate_Classification.ipynb   # the full analysis
├── data/
│   └── cache/                # committed LLM caches -> keyless reproduction
│       ├── zeroshot/         # GPT-4o and GPT-5.5 zero-shot predictions
│       ├── fewshot/          # few-shot predictions and the k-curve
│       └── generated/        # LLM-generated synthetic training data
├── outputs/                  # written at runtime (gitignored)
│   ├── figures/              # PNG figures (descriptive names, e.g. master_comparison.png)
│   └── tables/               # exported CSV / JSON tables
├── requirements.txt
└── README.md
```

## Setup

Python 3.10 or newer.

```bash
git clone https://github.com/Michaeldg94/greenwashing-detection-nlp.git
cd greenwashing-detection-nlp
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```

The dataset and every model (DistilRoBERTa, DeBERTa-v3 NLI, ClimateBERT, DistilBERT) download automatically from the Hugging Face Hub on first run. A GPU is optional: the notebook keeps `FAST_MODE = True`, so it also finishes on a CPU, just more slowly.

## Run

```bash
jupyter lab        # or: jupyter notebook
```

Open `notebooks/Armour_Canal_Goncalves_Guinea_Climate_Classification.ipynb` and run all cells top to bottom. Figures are written to `outputs/figures/`; exported CSV and JSON tables go to `outputs/tables/`.

The GPT-4o and GPT-5.5 sections read the cached predictions shipped under `data/cache/`, so the whole notebook reproduces with no API key and no cost.

## Optional: regenerate the LLM results yourself

Only needed if you want to recompute the GPT-4o and GPT-5.5 predictions instead of using the bundled caches. Provide an OpenAI key with access to those models:

```bash
cp .env.example .env     # then edit .env and set your key
```

Delete the relevant CSVs under `data/cache/` to force a fresh run, then rerun the notebook. Without a key the LLM cells fall back to the caches.
