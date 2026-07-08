# Contradiction-Aware Sparse Memory (CASM) Finetuning for Continual Learning in LLMs

**Graduate research report — CSCI 566: Deep Learning and Its Applications, University of Southern California (2025)**

📄 **[Read the full paper (PDF)](./CASM_Continual_Learning_Report.pdf)** · 💻 **[Code repository](https://github.com/athirai-s/Continual-Learning)**

## Abstract

Large Language Models perform well across many tasks but remain static after deployment: as facts change over time, naive fine-tuning leads to catastrophic forgetting. We propose **CASM (Contradiction-Aware Sparse Memory) Finetuning**, a continual-learning framework that models knowledge as versioned and time-scoped. CASM augments a frozen LLM with a bank of trainable sparse memory slots, detects contradictions between new and prior knowledge, and routes time-scoped queries to the appropriate knowledge version at inference time.

We evaluate CASM against full fine-tuning, LoRA, and a single-memory sparse baseline (SMF) on temporally structured factual updates (TemporalWiki + a controlled synthetic benchmark) using Llama 3.2 at 1B and 3B scale. Isolating updates in sparse memory significantly outperforms full fine-tuning and LoRA on continual factual learning. Under limited data and compute, the simpler SMF baseline achieves higher overall stability than CASM — an honest negative result suggesting that versioning and routing fragment the training signal in low-data regimes, and that contradiction-aware versioning likely needs larger-scale training to realize its benefits.

## Authors

Lydia Chatziioannou, Pratyush Lahane, Cynthia Liu, Ramya Krishnan, Aakriti Shah, Athirai Shanmugam, Rylan Wade

## My contributions (Pratyush Lahane)

- Co-defined the architecture of the CASM continual-learning training pipeline
- Ran LoRA fine-tuning experiments on Llama 3.2 1B (Google Colab / A100)
- Made adjustments to the synthetic-data slot-assignment logic and authored an updated synthetic CASM training script
- Ran the initial continual-learning experiments on the TSQA and TGQA datasets before the team's pivot to TemporalWiki
- Co-presented the project

Full per-member contributions are listed in Appendix B of the paper.

## Key results (1B scale, Synthetic TemporalWiki)

| Method | Avg. Plasticity | Avg. Stability |
|---|---|---|
| Full fine-tuning | 0.089 | 0.139 |
| LoRA | 0.138 | 0.221 |
| SMF | **0.591** | **0.482** |
| CASM (ours) | 0.329 (peak 0.680) | 0.258 |

**Takeaway:** sparse, isolated memory updates are the dominant driver of continual-learning performance in this regime; explicit versioning and routing add optimization challenges that require more data and compute to pay off.
