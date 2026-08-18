# Week 7/8 — Encoder-Decoder Machine Translation (English → French)

TECH 405 — Artificial Neural Network and Deep Learning

## Project structure

```
week_8_project/
├── Backend/
│   ├── model.py       # EncoderRNN, BahdanauAttention, AttnDecoderRNN
│   ├── data.py        # Kaggle download (kagglehub), Tatoeba supplement, vocab
│   ├── train.py        # trains the model, saves it to model/, plots loss
│   ├── app.py           # Flask server — loads the trained model, serves the frontend
│   └── model/           # created by train.py (encoder.pt, decoder.pt, vocab.pkl)
├── Front/
│   └── index.html      # the web UI (served by Backend/app.py)
├── requirements.txt
├── README.md
└── .gitignore
```

The Backend serves the Front folder directly (`app.py` points Flask's template/static
folder at `../Front`), so you only ever run commands from inside `Backend/`.

## Setup

1. Open this `week_8_project` folder in Cursor / VS Code.
2. Open a terminal and create a virtual environment **at the project root**:
   ```
   python -m venv venv
   venv\Scripts\activate      # Windows
   source venv/bin/activate   # macOS/Linux
   pip install -r requirements.txt
   ```

## Step 1 — Train the model

```
cd Backend
python train.py
```
This downloads the Kaggle English-French dataset (`dhruvildave/en-fr-translation-dataset`)
via `kagglehub`, merges Tatoeba short conversational sentences, trains for 20 epochs
on 50k pairs by default, and saves:
- `Backend/training_loss.png` — the loss curve (use this in your report)
- `Backend/model/encoder.pt`, `decoder.pt`, `vocab.pkl` — the trained model, used by app.py

Prints 5 sample translations to the terminal at the end — copy those for the report too.

Faster test run: `python train.py --limit 20000 --epochs 10`

Full corpus (very slow on CPU): `python train.py --limit 0`

## Step 2 — Run the frontend

```
python app.py
```
(still from inside `Backend/`)

Open **http://127.0.0.1:5000** — type an English sentence, click Translate. The page itself
is served straight from `Front/index.html`.

## Step 3 — Publish to GitHub

From the project root (`week_8_project/`):
```
git init
git add .
git commit -m "Week 7/8: Encoder-decoder machine translation"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```
