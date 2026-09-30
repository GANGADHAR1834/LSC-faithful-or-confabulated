# Lexical semantic change detection

This project looks at how word meanings change over time.

In simple terms, it asks: when a word is used in older texts and newer texts, does its meaning stay the same, or does it gain a new sense? The project also tries to explain the new meaning in a clear way.

This repository includes the data, helper scripts, baseline methods, and result files used in the AXOLOTL shared task.

## What this project is about

The goal is to study words across time and identify:

- words that keep their old meaning,
- words that gain a new meaning,
- and short explanations for those new meanings.

This is useful for language research, historical text analysis, and dictionary work.

## Project folders

- `data/` - datasets for the task, including training, development, and test examples
- `code/` - evaluation scripts and baseline models
- `results/` - leaderboard files and summary results
- `example.md` - a short example showing the task in plain language
- `predictions_*.tsv` - example prediction outputs

## Main idea

The task is divided into two parts:

1. Find new word meanings in later texts.
2. Write a simple description for each new meaning.

For example, a word may have one meaning in older writing and a different one in newer writing. The system needs to notice that change and explain it.

## Running the repository

Run the commands below from the repository root. Python 3.9 or newer is recommended.

### 1. Create an environment and install dependencies

On macOS or Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r code/requirements.txt
```

On Windows PowerShell:

```powershell
py -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r code/requirements.txt
```

The first Track 1 baseline run downloads its Hugging Face model automatically. The baselines use a GPU when CUDA-enabled PyTorch is available; otherwise they run on the CPU.

### 2. Run and evaluate the Track 1 baseline

This example runs the baseline on the Finnish development set and writes predictions to `predictions_fi.tsv`:

```bash
python code/baselines/baseline_track1.py \
  --test data/finnish/axolotl.dev.fi.tsv \
  --pred predictions_fi.tsv
```

Evaluate the predictions with the Track 1 scorer:

```bash
python code/evaluation/scorer_track1.py \
  --gold data/finnish/axolotl.dev.fi.tsv \
  --pred predictions_fi.tsv \
  --output track1_result.txt
```

For Russian, use these paths instead:

```bash
python code/baselines/baseline_track1.py \
  --test data/russian/axolotl.dev.ru.tsv \
  --pred predictions_ru.tsv

python code/evaluation/scorer_track1.py \
  --gold data/russian/axolotl.dev.ru.tsv \
  --pred predictions_ru.tsv \
  --output track1_result_ru.txt
```

### 3. Run and evaluate the Track 2 baseline

Track 2 predicts explanations for novel senses. A minimal Finnish training and evaluation run is:

```bash
python code/baselines/baseline_track2.py \
  --train_data data/finnish/axolotl.train.fi.tsv \
  --pretrain_data data/russian/axolotl.train.ru.tsv \
  --test_data data/finnish/axolotl.dev.fi.tsv \
  --predictions_file predictions_fi.track2.tsv
```

Evaluate the Track 2 predictions. Its scorer expects the submission, reference, and output paths positionally:

```bash
python code/evaluation/scorer_track2.py \
  predictions_fi.track2.tsv \
  data/finnish/axolotl.dev.fi.tsv \
  track2_result.txt
```

You can reduce the runtime while testing the Track 2 pipeline by adding, for example, `--debug_samples 20`.

### 4. Run the optional WSD baselines

The WSD baseline runner requires Bash, GNU Parallel, `curl`, and `unzip`. From the repository root, run:

```bash
cd code/baselines
bash run_wsdbaselines.sh
```

Results are written under `code/baselines/baseline_scores/` and the summary table is written to `code/baselines/wsdbaselines.scores.tsv`.

On Windows, run this section in WSL or another Bash-compatible environment.

### 5. Use the scorers with your own predictions

Track 1 predictions must be TSV files with the same row order and usage information as the reference file. Score them with:

```bash
python code/evaluation/scorer_track1.py \
  --gold path/to/reference.tsv \
  --pred path/to/predictions.tsv \
  --output path/to/track1_result.txt
```

Track 2 predictions are scored with:

```bash
python code/evaluation/scorer_track2.py \
  path/to/predictions.tsv \
  path/to/reference.tsv \
  path/to/track2_result.txt
```

The test files in `data/test/` and the German surprise set do not provide gold labels for local scoring. Use the Finnish and Russian development files for local evaluation. German is intended for surprise-language evaluation.

## Quick start

If you only want to explore the repository:

- look in `data/` for the language datasets,
- check `code/evaluation/` for scoring scripts,
- and use `code/baselines/` to see simple starting methods.

## Results

The current result files are stored in the `results/` folder. They include leaderboards and comparison tables.

## Data structure

The training and development files are tab-separated-values (TSV) files. Each row corresponds to one usage example. The main columns are:

- `usage_id` - unique usage identifier
- `word` - target headword
- `orth` - target word in an old spelling, when applicable
- `sense_id` - sense identifier
- `gloss` - definition of the sense
- `example` - usage example
- `indices_target_token` - character offsets for the target word, when available
- `date` - coarse-grained date of the usage
- `period` - either `old` or `new`

The test splits contain empty `sense_id` and `gloss` fields for new-period usages. The task is to predict sense IDs for Track 1 and definitions for novel senses in Track 2.

## Notes

This is a research project, so some terminology is technical, but the central idea is simple: study how word meanings change across time.

The repository is part of the AXOLOTL shared task for explainable semantic change modeling.
