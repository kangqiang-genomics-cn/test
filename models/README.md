# StrainDNA

## Code Structure and Usage Guide

This repository contains the implementation of StrainDNA, a foundation model for genomic sequence analysis. The code allows you to run inference on genetic sequences and reproduce our experimental results.

### Repository Structure

```
.
├── HuggingFace/              # Model architecture implementation
│   ├── configuration_glm.py  # Model configuration 
│   ├── modeling_glm.py       # Main model implementation
│   └── ...
├── test_data/                # Sample test data
│   └── demo.csv             # Example gene sequence data
├── dnaglm.py                 # Main inference script
├── run_dnaglm.sh             # Run script
└── requirements.txt          # Dependencies
```

### Requirements

The code requires Python 3.8+ and CUDA 12.0+. To install dependencies:

```bash
pip install -r requirements.txt
```

### Running Inference

To run inference on a DNA sequence:

1. Prepare your sequence data in CSV format with columns:
   - `unique_id`: Unique identifier for each sequence
   - `nt_seq`: Nucleotide sequence
   - `genome_id`: Unique identifier for each genome

2. Run the inference script:

```bash
bash run_dnaglm.sh
```

Or customize the run parameters:

```bash
python dnaglm.py --csv_path ./test_data/brca1.csv \
                 --task_name custom_task \
                 --model_path ./HuggingFace \
                 --ckpt_path ./checkpoint/StrainDNA_470M/model_states.pt \
                 --batch_size 1 \
                 --save_dir ./results
```

### Key Parameters

- `--csv_path`: Path to the input CSV file containing sequences
- `--task_name`: Name for the inference task (used for output files)
- `--max_seq_len`: Maximum sequence length (default: 2000)
- `--batch_size`: Batch size for inference
- `--ckpt_path`: Path to model checkpoint

### Output

The inference results will be saved in the `--save_dir` directory (default: `./results`) as a CSV file containing perplexity scores and other metrics for each sequence.