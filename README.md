# Starcoder2-3B Code Repair - v2 (Improved)

Fine-tuned `bigcode/starcoder2-3b` with QLoRA on a Python bug-fixing dataset.
v2 fixes: proper loss masking, no comment stripping, generation cleanup.

## Setup
- Base model: bigcode/starcoder2-3b
- Fine-tuning: QLoRA (4-bit NF4, r=16, alpha=16)
- Max sequence length: 768 tokens
- Hardware: 2x Tesla T4 (15GB each)

## Dataset
Custom hybrid dataset. Subset used for fast iteration.
- Train: 1,000 samples
- Validation: 200 samples
- Test: 200 samples

## Checkpoint Selection
Best checkpoint: step 120 (lowest eval loss).

| Checkpoint | Eval Loss |
|------------|-----------|
| 40 | 0.1745 |
| 80 | 0.1770 |
| **120** | **0.1666** |
| 160 | 0.1688 |

## Evaluation Results (Test Set, 200 samples)

| Metric | v1 (broken) | v2 (fixed) |
|--------|-------------|-------------|
| Exact Match | 0.0% | **1.5%** |
| Corpus BLEU | 13.9 | **32.9** |
| ROUGE-1 | — | **52.2** |
| ROUGE-2 | — | **47.1** |
| ROUGE-L | — | **51.4** |

## Known Issues
- Model hallucinates additional examples after the fix (38/200 samples).
- Post-processing extracts first fix only — real fix is to add stop token during training.

## Files
- `evaluation_results_v2.csv`: Per-sample predictions with metrics
- `merged_best/`: Merged best checkpoint (FP16)
- `starcoder2-3b-v2/`: Training checkpoints
