# Lexical semantic change detection

This project looks at how word meanings change over time.

In simple terms, it asks: when a word is used in older texts and newer texts, does its meaning stay the same, or does it gain a new sense? The project also tries to explain the new meaning in a clear way.

This repository includes the data, helper scripts, baseline methods, and result files used in the shared task.

## What this project is about

The goal is to study words across time and identify:

- words that keep their old meaning,
- words that gain a new meaning,
- and short explanations for those new meanings.

This is useful for language research, historical text analysis, and dictionary work.

## Project folders

- `data/` — datasets for the task, including training, development, and test examples
- `code/` — evaluation scripts and baseline models
- `results/` — leaderboard files and summary results
- `example.md` — a short example showing the task in plain language
- `predictions_*.tsv` — example prediction outputs

## Main idea

The task is divided into two parts:

1. Find new word meanings in later texts
2. Write a simple description for each new meaning

For example, a word may have one meaning in older writing and a different one in newer writing. The system needs to notice that change and explain it.

## Quick start

If you want to explore the repo:

- look in `data/` for the language datasets,
- check `code/evaluation/` for scoring scripts,
- and use `code/baselines/` to see simple starting methods.

## Results

The current result files are stored in the `results/` folder. They include leaderboards and comparison tables.

## Notes

This is a research project, so some terminology is technical, but the idea is simple: we are studying meaning changes in words across time.

If you want a more detailed technical description, the full project background and formal task setup are described in the papers and links provided in the repository materials.

---

This repository is part of the AXOLOTL shared task for explainable semantic change modeling.
