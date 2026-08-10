# Starcoder2-3B Code Repair - v3 Final Results

Fine-tuned `bigcode/starcoder2-3b` with QLoRA on Python bug-fixing dataset.
v3: stop token (`<|endoftext|>`), full 20k dataset, max_seq=1024.

## Best Checkpoint
Step 2200 (val_loss=0.170352)

## Full Dataset Results (2510 samples)

| Metric | Validation | Test |
|--------|-----------|------|
| Exact Match | 16.5% | 16.2% |
| Corpus BLEU | 88.8 | 89.7 |
| Per-sample BLEU (mean) | 79.1 | — |
| Per-sample BLEU (median) | 83.0 | — |
| ROUGE-1 | 89.0 | 89.0 |
| ROUGE-2 | 82.5 | 82.4 |
| ROUGE-L | 88.5 | 88.4 |
| Edit Ratio (mean) | 0.840 | 0.840 |
| Edit Ratio (median) | 0.873 | 0.874 |
| Prompt Contamination | 0% | 0% |

## Exact Match by Bug Type (Test)

| Bug Type | Count | EM % |
|----------|-------|------|
| build_package_merge | 55 | 72.7% |
| unknown | 480 | 48.8% |
| algorithm | 107 | 43.9% |
| checking | 53 | 39.6% |
| timing_serialization | 28 | 39.3% |
| assignment | 56 | 28.6% |
| reference | 17 | 23.5% |
| logic | 87 | 5.7% |
| other | 1548 | 1.9% |
| type | 69 | 0.0% |
| syntax | 10 | 0.0% |

## Progress

| Version | Changes | Test EM | BLEU |
|---------|---------|---------|------|
| v1 | Broken loss masking, no stop token | 0.0% | 13.9 |
| v2 | Fixed masking, 1k subset | 1.5% | 32.9 |
| v3 | Stop token, full 20k dataset, seq_len=1024 | **16.2%** | **89.7** |

## Key Improvements in v3
- `<|endoftext|>` stop token eliminated prompt hallucination (88% → 0%)
- Full dataset training improved generalization
- Longer sequences (1024) reduced truncation to 1.2%

## Limitations
- 62% of test samples are labeled "other" with only 1.9% EM — needs investigation
- Syntax and type bugs get 0% EM — may need targeted data augmentation

## Files
- `val_results_full.csv`: Full validation predictions with all metrics + bug types
- `test_results_full.csv`: Full test predictions with all metrics + bug types
- `checkpoint-2200/`: LoRA adapter weights
