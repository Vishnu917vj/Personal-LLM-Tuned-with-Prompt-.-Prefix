# Personalized LLM Optimization using Prompt Tuning and Prefix Tuning

## Overview

This project explores **Parameter-Efficient Fine-Tuning (PEFT)** techniques for personalizing a Large Language Model while keeping computational and storage costs low.

Instead of training a model from scratch, I first selected my best-performing personalized model obtained through **Full Supervised Fine-Tuning (SFT)** and then applied two lightweight PEFT techniques:

- Prompt Tuning
- Prefix Tuning

The objective was to investigate whether additional personalization can be achieved by training only a small number of parameters while keeping the backbone model frozen.

---

## Base Model

Both Prompt Tuning and Prefix Tuning were performed on top of my personalized SFT model available on Hugging Face.

### Base SFT Model

**Hugging Face Repository**

https://huggingface.co/vishnuamarapu/Full-Fine-Tuning-Qwen-2.5-0.5B-instruct-sft

This model was selected because it achieved the best overall performance among all personalization approaches I previously implemented.

---

## Previous Personalization Experiments

Before starting this project, multiple personalization techniques were explored.

| Method | Status |
|---------|--------|
| Full Fine-Tuning (Trainer) | ✅ |
| LoRA | ✅ |
| QLoRA | ✅ |
| Prompt Tuning | ✅ |
| Prefix Tuning | ✅ |

Among these, the **Full Fine-Tuning (SFT)** model demonstrated the strongest overall performance and was therefore chosen as the foundation for further PEFT experiments.

---

# Project Goals

The main objectives were:

- Explore lightweight personalization techniques.
- Keep the backbone language model frozen.
- Train only a very small number of additional parameters.
- Compare different PEFT methods on the same personalized dataset.
- Reduce storage and training cost while preserving personalization quality.

---

# Prompt Tuning

Prompt Tuning learns a set of **virtual prompt embeddings** that are prepended to every input while the underlying model remains frozen.

Architecture:

```
User Question
      │
      ▼

Virtual Prompt Embeddings
      │
      ▼

Frozen SFT Model
      │
      ▼

Generated Response
```

### Hugging Face Adapter

https://huggingface.co/vishnuamarapu/Full-Fine-Tuning-Qwen-2.5-0.5B-tuned-prompts

---

# Prefix Tuning

Prefix Tuning learns trainable **prefix key/value vectors** for every transformer layer while keeping the language model weights frozen.

Architecture:

```
User Question
      │
      ▼

Learned Prefix Key/Value States
      │
      ▼

Frozen SFT Model
      │
      ▼

Generated Response
```

### Hugging Face Adapter

https://huggingface.co/vishnuamarapu/Full-Fine-Tuning-Qwen-2.5-0.5B-instruct-sft-prefix-tuned

---

# Dataset

The personalized dataset used for training is included in this repository.

It contains question-answer pairs about my personal information, including:

- Personal Details
- Education
- Skills
- Projects
- Internships
- Technical Experience
- Career Information

The dataset is provided in Excel format and was used for both Prompt Tuning and Prefix Tuning.

---

# Repository Structure

```
.
├── Prompt_Tuning.ipynb
├── Prefix_Tuning.ipynb
├── dataset.xlsx
├── train.xlsx
├── validation.csv
├── README.md
```

---

# Notebooks

## Prompt_Tuning.ipynb

Contains the complete implementation of Prompt Tuning including:

- Loading the personalized SFT model
- Creating Prompt Tuning configuration
- Dataset preprocessing
- Training
- Evaluation
- Saving adapter
- Uploading adapter to Hugging Face
- Inference examples

---

## Prefix_Tuning.ipynb

Contains the complete implementation of Prefix Tuning including:

- Loading the personalized SFT model
- Creating Prefix Tuning configuration
- Dataset preprocessing
- Training
- Evaluation
- Saving adapter
- Uploading adapter to Hugging Face
- Inference examples

---

# Technologies Used

- Python
- PyTorch
- Hugging Face Transformers
- Hugging Face PEFT
- Hugging Face Datasets
- Accelerate
- TRL
- Google Colab

---

# Future Work

Possible future directions include:

- P-Tuning v2
- Adapter Fusion
- Hybrid Prompt + Prefix architectures
- Multi-task personalization
- Retrieval-Augmented Generation (RAG)
- Personalized memory systems

---

# Acknowledgements

This project builds upon the open-source ecosystem provided by:

- Hugging Face
- PEFT
- Transformers
- Qwen Team

---

# Author

**Vishnu Amarapu**

AI Engineer | Machine Learning Engineer | MLOps Engineer

GitHub:
https://github.com/Vishnu917vj

Hugging Face:
https://huggingface.co/vishnuamarapu
