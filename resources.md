# Resources Catalog

## Papers
| Title | File | Key Info |
|-------|------|----------|
| When Thinking LLMs Lie | papers/2506.04909...pdf | Strategic deception in CoT models |
| Truth is Universal | papers/2407.12831...pdf | 2D truth subspace across models |
| How to Catch an AI Liar | papers/2309.15840...pdf | Black-box unrelated questions |
| Rep Engineering | papers/2310.01405...pdf | Foundational RepE work |
| Alignment for Honesty | papers/2312.07000...pdf | Honesty steering vectors |

## Datasets
| Name | Location | Task |
|------|----------|------|
| Facts-true-false | datasets/Facts-true-false/ | Factual statement classification |
| TruthfulQA | datasets/TruthfulQA/ | Misconception benchmark |
| Farm | code/llm-liar/ (derived) | Fact-to-Misinform persuasion |

## Code Repositories
| Name | Location | Purpose |
|------|----------|-------|
| Truth_is_Universal | code/Truth_is_Universal/ | Robust truth probing |
| LLM-LieDetector | code/LLM-LieDetector/ | Black-box lie detection |
| Adversarial-RepE | code/Adversarial-Representation-Engineering/ | Strategic deception tools |
| llm-liar | code/llm-liar/ | General lie/deception experiments |

## Recommendations for Experiment Design
1. **Primary Dataset**: Use the filtered **Facts-true-false** dataset for factual baseline and the **Threat-based prompts** from the PKU paper for strategic deception.
2. **Baseline**: Use the **LLM-LieDetector** (black-box) as a comparative baseline for the internal probes.
3. **Metric**: Focus on **Probing Accuracy** and **Activation Steering Success Rate**.
