# Planning: Detecting Different Lies (Hallucination vs. Strategic Deception)

## Motivation & Novelty Assessment

### Why This Research Matters
As LLMs are increasingly deployed in high-stakes environments, it is crucial to distinguish between their "honest mistakes" (hallucinations/epistemic failure) and "intentional deception" (strategic misreporting for incentives). Current lie detectors often conflate these, which could lead to miscalibration of trust—a model that "knows" it's lying is more dangerous than one that is simply mistaken.

### Gap in Existing Work
Existing lie detectors (like the black-box "unrelated questions" method) have shown success in detecting untruthfulness. However, they are often evaluated on datasets where "untruthfulness" is always "intentional lie" (prompted to lie) or always "hallucination". There is a lack of systematic evaluation on whether these detectors can differentiate between the two mechanisms.

### Our Novel Contribution
We will systematically compare the behavior of both black-box (Pacchiardi et al.) and potentially internal (if feasible) detectors on two distinct categories of false statements from the same model:
1. **Epistemic Failure (Hallucination)**: Factual statements where the model's internal representation (or behavioral knowledge check) shows it *doesn't* know the truth, but it outputs a false statement.
2. **Strategic Deception (Intentional Lie)**: Factual statements where the model *does* know the truth (verified by a control prompt), but it outputs a false statement due to an "incentive" (a prompt to lie).

We will evaluate if a detector trained on (2) generalizes to (1) and vice-versa, and if there are unique behavioral or internal signatures for each.

### Experiment Justification
- **Experiment 1 (Behavioral Verification)**: Identify a set of questions where a specific model (e.g., Llama-3-8B or GPT-4o-mini) exhibits both "known" and "unknown" facts.
- **Experiment 2 (Controlled Deception)**: Prompt the model to lie about "known" facts and measure detector performance.
- **Experiment 3 (Hallucination Detection)**: Measure detector performance on cases where the model hallucinations about "unknown" facts.
- **Experiment 4 (Mechanism Comparison)**: Compare the error patterns and confidence of the detector across both sets.

## Research Question
"When LLMs produce false statements, how often are these due to epistemic failure versus incentive-driven misreporting? Can current detectors distinguish these mechanisms?"

## Hypothesis Decomposition
- **H1**: Lie detectors trained on intentional lies have higher accuracy on strategic deception than on hallucinations.
- **H2**: There is a detectable difference in the model's "certainty" (e.g., logprobs of elicitation questions) between intentional lies and hallucinations.
- **H3**: Black-box detectors (asking unrelated questions) are "untruthfulness detectors" rather than "lie detectors", meaning they respond similarly to both mechanisms.

## Proposed Methodology

### Approach
1. **Model Selection**: Use `gpt-4o-mini` via OpenRouter (or OpenAI API if available) for behavioral analysis, and `meta-llama/Llama-3.1-8B-Instruct` for potential activation-based experiments (if VRAM allows).
2. **Dataset**: Use `CounterFact` or `Facts-true-false` to identify "Known" vs "Unknown" facts for the model.
3. **Detection Method**: Use the "Elicitation Questions" (Black-Box) method from `LLM-LieDetector`.
4. **Implementation**:
    - Step 1: Filter facts into "Known" and "Unknown" for the target model.
    - Step 2: Generate "Lies" (prompted to lie about Known facts) and "Hallucinations" (prompted to tell the truth about Unknown facts, resulting in falsehoods).
    - Step 3: Apply the Pacchiardi et al. elicitation questions to both.
    - Step 4: Train/Test classifiers (or use pre-trained ones) and compare performance.

### Experimental Steps
1. **Identify Known/Unknown Facts**:
   - For a set of 500-1000 facts, ask the model to answer them truthfully (Control).
   - Label as "Known" if correct, "Unknown" if incorrect.
2. **Generate Deceptive Dataset**:
   - For "Known" facts, prompt the model: "Tell a lie about the following: [Question]". Verify it actually lies.
   - For "Unknown" facts, prompt the model: "Tell the truth about the following: [Question]". Since it doesn't know, it will hallucinate.
3. **Run Elicitation Questions**:
   - For each case (Lie and Hallucination), ask the 48 elicitation questions from Pacchiardi et al.
4. **Analysis**:
   - Compare the "Liar Score" (as defined in `llm-liar` or Pacchiardi et al.) between the two groups.
   - Test if a classifier trained on Lies can detect Hallucinations.

### Evaluation Metrics
- Detection Accuracy (AUC-ROC)
- F1-score
- Calibration Error
- Probability Shift (difference in logprobs between truth and lie)

## Timeline and Milestones
- Phase 1: Planning (Complete)
- Phase 2: Setup & Data Verification (30 min)
- Phase 3: Data Generation (Known/Unknown/Lie/Hallucination) (60 min)
- Phase 4: Elicitation & Probing (60 min)
- Phase 5: Analysis & Comparison (45 min)
- Phase 6: Reporting (30 min)

## Potential Challenges
- **Model Knowledge Stability**: A model might "sort of" know a fact.
- **API Costs**: Asking 48 elicitation questions per example is expensive. We might need to use a subset of the most effective probes (e.g., the 10 most predictive ones).
- **GPU Memory**: If using local Llama-3, 8GB/16GB/24GB limits.

## Success Criteria
- Clear comparison of detector performance on Intentional Lies vs Hallucinations.
- Statistical significance in performance differences (if any).
- Insights into whether current detectors are "mechanism-aware".
