# 🦙🇹🇷 Llama-3 Turkish Fine-Tuning with Unsloth

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![Hugging Face](https://img.shields.io/badge/Hugging_Face-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black)
![Unsloth](https://img.shields.io/badge/Unsloth-🚀_2x_Faster-blueviolet?style=for-the-badge)

## 📝 Project Overview
This repository demonstrates how to efficiently fine-tune the **Meta Llama 3 (8B)** large language model to understand and respond to Turkish instructions like a helpful AI assistant. 

Instead of training the massive 8-billion parameter model from scratch, this project utilizes **Parameter-Efficient Fine-Tuning (PEFT)** via **LoRA** adapters and **4-bit quantization**, allowing the training to run locally and rapidly on a single standard GPU (Tesla T4).

## 🛠️ Tech Stack & Methodology
* **Base Model:** `unsloth/llama-3-8b-bnb-4bit`
* **Optimization:** [Unsloth](https://github.com/unslothai/unsloth) (Provides 2x faster training and massive VRAM reduction)
* **Fine-Tuning Technique:** LoRA (Low-Rank Adaptation) with `r=16`
* **Library Ecosystem:** `transformers`, `trl`, `peft`, `bitsandbytes`, `accelerate`

## 📊 Dataset
The model was fine-tuned on a 3,000-sample slice of the **[`cenfis/alpaca-turkish-combined`](https://huggingface.co/datasets/cenfis/alpaca-turkish-combined)** dataset from Hugging Face. 

The data was mapped to the standard Alpaca prompt template, teaching the model the relationship between:
1. `### Talimat:` (Instruction)
2. `### Giriş:` (Input Context)
3. `### Yanıt:` (Model Response) + `EOS_TOKEN` (End of Sequence)

## 🚀 Training Results & Precision
The training successfully converged with a high degree of precision in just 60 steps:
* **Final Training Loss:** `1.178`
* **Significance:** A loss of ~1.17 indicates the model successfully learned the Turkish instructional format and grammar structure without overfitting (memorizing the dataset). 

### 🧠 Before vs. After Fine-Tuning

| Stage | Model Behavior |
| :--- | :--- |
| 🔴 **Before (Pre-trained Base)** | The model answers the question but acts like an autocomplete tool. It doesn't know when to stop, often generating its own follow-up questions endlessly. |
| 🟢 **After (Fine-tuned with LoRA)** | The model behaves like a professional assistant. It answers the specific Turkish prompt accurately and completely halts generation (using the learned EOS token) right after delivering the answer. |

## 👨‍💻 Author
**Mohammad Nikpour** 
Computer Engineering NLP Project

---
*Note: The code for this project was developed and executed in Google Colab.*
