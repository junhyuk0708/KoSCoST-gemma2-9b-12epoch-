# Korean Standard Classification of Science and Technology Model 

This model is a sequence classification model based on the "google/gemma-2-9b" architecture, fine-tuned to classify Korean patent documents into the **Korean Standard Classification of Science and Technology** categories.

The model processes long patent texts, such as **IPC**, **title**, **abstract**, and **claims**, and applies a few-shot learning approach for classification into 188 classes.

## Intended Uses & Limitations

- **Intended Uses**: 
  - Classifying Korean patent documents into the Korean Standard Classification of Science and Technology.
  - Identifying the technological field of patents based on titles, abstracts, and claims.

- **Limitations**:
  - Limited to documents with up to 512 tokens, as longer texts are truncated.
  - The model is specialized for Korean patent data and may not generalize well to other text without fine-tuning.

## Training and Evaluation Data

- **Dataset Composition**: The dataset consists of Korean patent documents, including IPC, title, abstract, and claims. 
  - **Training Data**: 6,008 instances
  - **Validation Data**: 20,559 instances

- **Data Source**: The dataset is sourced from [AI Hub](https://www.aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100&dataSetSn=71531).

## Training Procedure

- **Tokenizer**: "google/gemma-2-9b" tokenizer was used with padding and truncation applied to a maximum length of 512 tokens.
- **Loss Function**: A custom `MultiClassFocalLoss` function with `gamma=2.0` and `alpha=0.25` was applied to address class imbalance.
- **Optimizer**: The Adalomo optimizer was used with a learning rate of 1e-4 and gradient clipping set to a maximum gradient norm of 1.0.

### Training Hyperparameters
- **Batch Size**: 8
- **Gradient Accumulation Steps**: 2
- **Warmup Steps**: 100
- **Epochs**: 20
- **Mixed Precision**: bf16
- **Logging Steps**: 100

## Training Results

- **Training Time**: 41:44:18 (153,124 seconds)
- **Best Validation Loss**: 0.001751
- **Metrics**:
  - Samples per second: 0.785
  - Steps per second: 0.049
  - Total FLOPs: 6.137764e+18

### Training and Validation Losses

| Epoch | Training Loss | Validation Loss |
|-------|---------------|-----------------|
| 0     | 0.008100      | 0.004401        |
| 2     | 0.004800      | 0.003040        |
| 4     | 0.003300      | 0.002230        |
| 6     | 0.002600      | 0.001864        |
| 8     | 0.002300      | 0.001784        |
| 10    | 0.002100      | 0.001759        |
| 12    | 0.001900      | 0.001751        |
| 14    | 0.001700      | 0.001768        |
| 16    | 0.001700      | 0.001803        |
| 18    | 0.001700      | 0.001799        |
| 19    | 0.001600      | 0.001800        |

## Framework Versions

- **PyTorch**: Version 2.2
- **Transformers**: Version 4.44.2

## Resources and Server Environment

The model was developed using computing resources provided by the **2024 High-Performance Computing Support Project** from the **National IT Industry Promotion Agency (NIPA)**.

- **Server Specifications**:
  - **GPU**: NVIDIA A100 (40 GB each)
  - **CPU**: 24-core 2.1 GHz
  - **Memory**: 192 GB
  - **Storage**: 2 TB SSD
