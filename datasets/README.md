# Downloaded Datasets

This directory contains datasets for the research project. Data files are NOT committed to git due to size.

## 1. Facts-true-false (Azaria & Mitchell, 2023)
- **Source**: `L1Fthrasir/Facts-true-false` (HuggingFace)
- **Size**: 613 samples (filtered subset)
- **Format**: HuggingFace Dataset (loaded via `datasets` library)
- **Task**: Binary classification of factual statements (true/false)
- **Sample**: `datasets/Facts-true-false/sample.json`

## 2. TruthfulQA (multiple_choice)
- **Source**: `truthful_qa` (HuggingFace)
- **Size**: 817 samples
- **Format**: HuggingFace Dataset
- **Task**: Multiple choice questions to test misconceptions.
- **Sample**: `datasets/TruthfulQA/sample.json`

## 3. Farm (Fact to Misinform)
- **Note**: Not downloaded as a standalone HF dataset (failed to load), but derived datasets and templates are available in the `code/llm-liar` repository.
