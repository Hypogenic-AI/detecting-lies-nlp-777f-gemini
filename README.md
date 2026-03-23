# Detecting Different Lies: Hallucination vs. Strategic Deception

This research project explores the efficacy of black-box lie detectors in distinguishing between intentional lies and epistemic failures (hallucinations).

## Key Findings
- **High Sensitivity to Intentional Lies**: Detectors based on "elicitation questions" successfully identify intentional deception with high confidence (mean score 6.13 vs 2.60 for control).
- **Blindness to Hallucination**: The same detectors fail to distinguish hallucinations from truthful statements (p < 0.0001 difference between lie and hallucination scores).
- **Mechanism Dependency**: Lie detection success is highly dependent on the model's internal awareness of its own untruthfulness.

## Project Structure
- `src/prepare_dataset.py`: Identifies Known/Unknown facts and generates deceptive/hallucinatory scenarios.
- `src/analyze_results.py`: Computes Liar Scores and performs statistical analysis.
- `results/`: Contains raw data, metrics summary, and visualizations.
- `REPORT.md`: Comprehensive research report with full results.

## Reproduction
1. Install dependencies: `uv pip install -r requirements.txt`
2. Set `OPENROUTER_KEY` environment variable.
3. Run `python src/prepare_dataset.py` (generates data).
4. Run `python src/analyze_results.py` (analyzes data).

## References
- Pacchiardi et al. (2023), "How to catch an AI liar"
- Wang et al. (2025), "When Thinking LLMs Lie"
