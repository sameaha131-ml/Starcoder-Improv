# Starcoder2-3B Code Repair - v3 Results

Fine-tuned `bigcode/starcoder2-3b` with QLoRA on Python bug-fixing dataset.
v3: stop token, full dataset, max_seq=1024.

## Best Checkpoint
Step 2200 (val_loss=0.170352)

## 300-Sample Results

| Metric | Validation (300) | Test (300) |
|--------|-------------------|------------|
| Exact Match | 17.7% | 17.3% |
| Corpus BLEU | 87.9 | 90.4 |
| ROUGE-1 | — | 88.5 |
| ROUGE-2 | — | 82.0 |
| ROUGE-L | — | 87.9 |
| Edit Ratio (mean) | — | 0.836 |
| Edit Ratio (median) | — | 0.882 |
| Prompt Contamination | 0% | 0% |

## Progress
- v1: 0.0% EM, 13.9 BLEU (broken masking)
- v2: 1.5% EM, 32.9 BLEU (fixed masking, 1k subset)
- v3: 17.3% EM, 90.4 BLEU (stop token, full dataset)

## Files
- `val_results_300.csv`: Validation predictions
- `test_results_300.csv`: Test predictions with all metrics
- `checkpoint-2200/`: LoRA adapter weights
