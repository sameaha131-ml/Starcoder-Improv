# Starcoder2-3B Code Repair - v3 (Stop Token + Full Dataset)

Fine-tuned `bigcode/starcoder2-3b` with QLoRA on Python bug-fixing dataset.
v3 adds stop token (`<|endoftext|>`) to prevent hallucination, trains on full dataset.

## Setup
- Base model: bigcode/starcoder2-3b
- Fine-tuning: QLoRA (4-bit NF4, r=16, alpha=16)
- Max sequence length: 1024 tokens
- Hardware: 2x Tesla T4 (15GB each)
- Effective batch size: 16

## Dataset
- Train: 20,077 samples
- Validation: 2,510 samples
- Test: 2,510 samples

## Training Log
| Step | Train Loss | Val Loss |
|------|-----------|----------|
| 200 | 0.248391 | 0.204368 |
| 400 | 0.167492 | 0.188170 |
| 600 | 0.149948 | 0.184889 |
| 800 | 0.146764 | 0.181425 |
| 1000 | 0.129240 | 0.180178 |
| 1200 | 0.133605 | 0.175672 |
| 1400 | 0.111735 | 0.176284 |
| 1600 | 0.133873 | 0.176963 |
| 1800 | 0.100462 | 0.172616 |
| 2000 | 0.103483 | 0.172639 |
| 2200 | 0.107015 | 0.170352 |
| 2400 | 0.091035 | 0.170024 |
| 2600 | 0.100047 | 0.171554 |
| 2800 | 0.083677 | 0.171930 |
| 3000 | 0.093338 | 0.170633 |

## Best Checkpoint
Step 2400: val_loss = 0.170024 (downloaded manually).
Step 2200: val_loss = 0.170352 (backup).

## Key Changes from v2
- Added `<|endoftext|>` stop token to fixed code in training data
- Full dataset (20k vs 1k)
- max_seq_length increased to 1024 (1.2% truncation)
- EOS token ID = 0 matches stop token

## Evaluation
Pending — will test checkpoint-2200 on 300 samples.

## Files
- `trainer_state.json`: Full training log
- `checkpoint-*/`: LoRA adapter weights
