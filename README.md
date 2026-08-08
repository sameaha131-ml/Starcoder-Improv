# Starcoder2-3B Code Repair - Improved Fine-tuning

Fine-tuning `bigcode/starcoder2-3b` with QLoRA on a Python bug-fixing dataset.
This is an improved version addressing issues found in the first training run.

## Changes from v1
- Proper loss masking (only compute loss on fixed code portion)
- No comment stripping during preprocessing
- Increased max sequence length to reduce truncation
- Generation-based validation during training (exact match monitoring)
- Smaller subset first (1000 train) for fast iteration

## Setup
- Base model: bigcode/starcoder2-3b
- Fine-tuning method: QLoRA (4-bit NF4, r=16, alpha=16)
- Hardware: Tesla T4 (15GB)
- Framework: PyTorch, HuggingFace Transformers, PEFT, bitsandbytes

## Dataset
Custom hybrid dataset of Python buggy/fixed code pairs.
- Train: 1,000 samples (subset for fast iteration)
- Validation: 200 samples
- Test: 200 samples

## Results
| Metric | Value |
|--------|-------|
| Exact Match Rate |     |
| Corpus BLEU |     |
| ROUGE-1 |     |
| ROUGE-L |     |

## Files
- `evaluation_results.csv`: Per-sample predictions with metrics
- `best_checkpoint/`: Best LoRA adapter weights
