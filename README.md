# Personalized LLM Optimization using Prompt Tuning and Prefix Tuning

## Overview

This repository explores **Parameter-Efficient Fine-Tuning (PEFT)** techniques for personalizing a Large Language Model while minimizing computational and storage costs.

The goal of this project is to investigate whether a well-personalized language model can be further optimized using lightweight PEFT methods without modifying the backbone model.

Instead of training a new model from scratch, I first selected my best-performing personalized model obtained through **Full Supervised Fine-Tuning (SFT)** and then used it as the foundation for two additional personalization experiments:

- Prompt Tuning
- Prefix Tuning

Both experiments were performed using the **same personalized dataset**, allowing a fair comparison between the two PEFT approaches.

---

# Project Workflow

The overall workflow followed in this project is shown below.

```
                         Qwen2.5-0.5B-Instruct
                                  │
                                  ▼
                     Full Supervised Fine-Tuning (SFT)
                                  │
                   Best Performing Personalized Model
                                  │
                ┌─────────────────┴─────────────────┐
                │                                   │
                ▼                                   ▼
         Prompt Tuning                      Prefix Tuning
                │                                   │
                ▼                                   ▼
      Prompt Adapter                     Prefix Adapter
```

---

# Why the SFT Model?

Before this project, I experimented with several personalization approaches using the same dataset.

The following models were trained and evaluated:

- Full Fine-Tuning (Trainer API)
- LoRA
- QLoRA

Among these approaches, the **Supervised Fine-Tuning (SFT)** model consistently produced the best responses for my personalized question-answering task.

Therefore, instead of using the original Qwen model, I selected the SFT model as the backbone for further PEFT experiments.

---

# Base Model

The following personalized SFT model was used as the starting point for both Prompt Tuning and Prefix Tuning.

**Hugging Face**

https://huggingface.co/vishnuamarapu/Full-Fine-Tuning-Qwen-2.5-0.5B-instruct-sft

---

# Prompt Tuning

Prompt Tuning keeps the language model completely frozen and learns only a small number of **virtual prompt embeddings**.

Architecture:

```
User Question
      │
      ▼

Virtual Prompt Embeddings
      │
      ▼

Frozen Personalized SFT Model
      │
      ▼

Generated Response
```

### Prompt Tuning Adapter

https://huggingface.co/vishnuamarapu/Full-Fine-Tuning-Qwen-2.5-0.5B-tuned-prompts

---

# Prefix Tuning

Prefix Tuning also freezes the backbone model but learns trainable **prefix key/value vectors** for every transformer layer.

Architecture:

```
User Question
      │
      ▼

Learned Prefix Key/Value States
      │
      ▼

Frozen Personalized SFT Model
      │
      ▼

Generated Response
```

### Prefix Tuning Adapter

https://huggingface.co/vishnuamarapu/Full-Fine-Tuning-Qwen-2.5-0.5B-instruct-sft-prefix-tuned

---

# Dataset

The personalized dataset used throughout this project is included in this repository.

It contains manually curated question-answer pairs describing my:

- Personal Information
- Education
- Skills
- Technical Stack
- Projects
- Internships
- Professional Experience
- Career Goals

The same dataset was used for:

- Supervised Fine-Tuning
- Prompt Tuning
- Prefix Tuning

to ensure consistency across experiments.

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

This notebook demonstrates the complete Prompt Tuning workflow.

It includes:

- Loading the personalized SFT model
- Creating the Prompt Tuning configuration
- Dataset preprocessing
- Model training
- Evaluation
- Saving the adapter
- Uploading the adapter to Hugging Face
- Running inference

---

## Prefix_Tuning.ipynb

This notebook demonstrates the complete Prefix Tuning workflow.

It includes:

- Loading the personalized SFT model
- Creating the Prefix Tuning configuration
- Dataset preprocessing
- Model training
- Evaluation
- Saving the adapter
- Uploading the adapter to Hugging Face
- Running inference

---

# Experimental Results

## Prompt Tuning

| Epoch | Training Loss | Validation Loss | Mean Token Accuracy |
|------:|--------------:|----------------:|--------------------:|
| 1 | 14.71 | 15.12 | 18.67% |
| 5 | 13.52 | 14.39 | 18.75% |
| 10 | 13.23 | 13.70 | 18.67% |
| 15 | 14.34 | 13.17 | 18.63% |
| 20 | **12.73** | **13.16** | **18.67%** |

---

## Prefix Tuning

| Epoch | Training Loss | Validation Loss | Mean Token Accuracy |
|------:|--------------:|----------------:|--------------------:|
| 1 | 1.68 | 1.02 | 86.63% |
| 5 | 0.65 | 0.41 | 91.92% |
| 10 | 0.42 | 0.26 | 94.12% |
| 15 | 0.22 | 0.18 | 95.69% |
| 20 | **0.17** | **0.15** | **96.39%** |

---

# Observations

- The SFT model served as a strong personalized foundation.
- Prompt Tuning successfully learned lightweight virtual prompt embeddings while keeping the SFT model frozen.
- Prefix Tuning converged more quickly during training and achieved substantially lower validation loss and higher mean token accuracy on the training dataset.
- Both PEFT methods produced lightweight adapters that are significantly smaller than a fully fine-tuned model.

**Note:** Training metrics are useful for understanding optimization behavior, but the final evaluation should also consider response quality, factual accuracy, and robustness on held-out personalized questions.

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

Possible future extensions include:

- P-Tuning v2
- LoRA on top of the personalized SFT model
- QLoRA on the personalized SFT model
- Adapter Fusion
- Retrieval-Augmented Generation (RAG)
- Long-term memory integration
- Multi-user personalization
- Comparative evaluation across multiple PEFT techniques

---

# Acknowledgements

This work builds upon the excellent open-source ecosystem provided by:

- Hugging Face
- Transformers
- PEFT
- Accelerate
- TRL
- Qwen Team

---

# Author

**Vishnu Amarapu**

AI Engineer | Machine Learning Engineer | MLOps Engineer

## GitHub

https://github.com/Vishnu917vj

## Hugging Face

https://huggingface.co/vishnuamarapu
