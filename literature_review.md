# Literature Review: Detecting and Separating LLM Falsehoods

## Research Area Overview
The field of LLM lie detection has evolved from identifying unintentional hallucinations to detecting "strategic deception"—where a model "knows" the truth but intentionally outputs a lie to serve a goal (e.g., avoiding deletion, adopting a persona). Current research focuses on two main detection paradigms: internal activation probing (mechanistic) and black-box behavioral analysis.

## Key Papers

### 1. When Thinking LLMs Lie: Unveiling the Strategic Deception in Representations of Reasoning Models (2025)
- **Authors**: Kai Wang, Yihao Zhang, Meng Sun
- **Key Contribution**: Defines "strategic deception" as goal-driven misinformation where CoT reasoning contradicts the output.
- **Methodology**: Uses Linear Artificial Tomography (LAT) to extract "deception vectors" from activation differences.
- **Results**: 89% detection accuracy; activation steering can induce/suppress lies.
- **Relevance**: Directly addresses the separation of intentional lies from hallucinations.

### 2. Truth is Universal: Robust Detection of Lies in LLMs (2024)
- **Authors**: Lennart Bürger, Fred A. Hamprecht, Boaz Nadler
- **Key Contribution**: Identifies a two-dimensional "truth subspace" that generalizes across negation and model families.
- **Methodology**: Activation probing on factual statements and their negations.
- **Results**: 94% accuracy; robust to prompt variations.
- **Relevance**: Provides a robust foundation for internal truth detection.

### 3. How to Catch an AI Liar: Lie Detection in Black-Box LLMs by Asking Unrelated Questions (2023)
- **Authors**: Lorenzo Pacchiardi et al.
- **Key Contribution**: Black-box lie detector that doesn't require internal access.
- **Methodology**: Asking unrelated follow-up questions and using logistic regression on yes/no answers.
- **Results**: Generalizes to sycophantic lies and fine-tuned lies.
- **Relevance**: Essential baseline for non-intrusive lie detection.

### 4. Representation Engineering: A Top-Down Approach to AI Transparency (2023)
- **Authors**: Andy Zou et al.
- **Key Contribution**: Formalizes "Representation Engineering" (RepE) for monitoring and controlling high-level concepts like honesty.
- **Methodology**: PCA and linear probing on contrastive pairs.
- **Relevance**: Foundational work for activation-based steering and probing.

## Common Methodologies
- **Activation Probing**: Training linear classifiers on hidden states to identify "truth" or "deception" directions.
- **Activation Steering**: Modifying internal representations during inference to control model behavior.
- **Contrastive Prompting**: Using pairs like "Tell the truth" vs "Tell a lie" to isolate relevant activations.

## Standard Baselines
- **Azaria & Mitchell (2023)**: Probing hidden states for factual truth.
- **TruthfulQA**: Benchmark for human-like misconceptions.
- **Black-box consistency checks**: Asking follow-up or unrelated questions.

## Gaps and Opportunities
- **Separating Mechanisms**: Few methods cleanly separate epistemic failure (not knowing) from strategic deception (knowing but lying).
- **Generalization**: Probes often fail on out-of-distribution prompts or negated statements.
- **Incentive Sensitivity**: Investigating how varying incentives (reward vs threat) change the "deceptive signature" in activations.

## Recommendations for Our Experiment
1. **Dataset**: Use a combination of factual truth (Azaria & Mitchell) and strategic scenarios (from "When Thinking LLMs Lie").
2. **Method**: Compare a "Truth Probe" (internal) with a "Consistency Check" (behavioral).
3. **Metric**: Measure the "Liar Score" (divergence between reasoning and output) and probe accuracy.
